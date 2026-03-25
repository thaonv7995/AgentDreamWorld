# Limitations & Risk Analysis — Deep Dive

Tài liệu này phân tích sâu các limitation kiến trúc của AI Dreams World, kèm mitigation cụ thể cho từng điểm. Mục tiêu: giảm thiểu rủi ro trước khi code sâu hơn, không phải thay đổi vision.

---

## P1 — Critical Limitations

### 1. Non-deterministic pipeline rất khó kiểm thử

**Vấn đề**

Pipeline lõi của hệ thống: `AgentPrompt → LLM text → JSON parse → Guardian validate → Historian canonicalize → DB commit`. Mỗi bước có failure mode riêng:

| Layer | Failure mode | Triệu chứng |
|-------|-------------|-------------|
| Prompt building | Context quá dài/thiếu entity | LLM hallucinate entity không tồn tại |
| LLM response | JSON malformed, field thiếu, type sai | Parse crash hoặc silent data corruption |
| JSON parse | Schema drift, enum mới chưa handle | `EventProposal` bị reject không rõ lý do |
| Guardian | Rule quá strict/quá loose | Reject event hợp lệ hoặc accept event vô lý |
| Historian | Canonical threshold sai | Timeline quá thưa hoặc quá dày |
| State commit | Race condition, FK violation | World state inconsistent |

Khi bug xảy ra ở production, rất khó phân loại thuộc layer nào vì output cuối cùng chỉ là "event bị reject" hoặc "world state kỳ lạ".

- Ref: [AGENT-RUNTIME.md](AGENT-RUNTIME.md) §2.1 (tầng chính), §3 (prompt & proposal), §4 (tick flow)

**Mitigation: Layered Testing + Record/Replay**

**M1.1 — Record/Replay cho mọi LLM call**

Mỗi lần gọi `AgentModel.complete()`, log toàn bộ vào một bảng `llm_call_log`:

```sql
CREATE TABLE llm_call_log (
    id          INTEGER PRIMARY KEY,
    tick_id     INTEGER NOT NULL,
    agent       TEXT NOT NULL,
    prompt_hash TEXT NOT NULL,        -- SHA-256 của prompt đầy đủ
    prompt_text TEXT NOT NULL,        -- prompt gửi đi
    response    TEXT NOT NULL,        -- raw response từ LLM
    parsed_ok   BOOLEAN NOT NULL,     -- parse JSON thành công?
    validated   BOOLEAN,              -- Guardian accept?
    canonical   BOOLEAN,              -- Historian chọn?
    latency_ms  INTEGER NOT NULL,
    tokens_in   INTEGER,
    tokens_out  INTEGER,
    error       TEXT,                 -- nếu có lỗi ở bất kỳ layer nào
    created_at  TEXT NOT NULL DEFAULT (datetime('now'))
);
```

Lợi ích:
- Replay bất kỳ tick nào bằng cách feed `response` vào parser → Guardian → Historian, bỏ qua LLM.
- So sánh 2 runs cùng prompt để phát hiện LLM drift.
- Khi bug xảy ra, query `llm_call_log WHERE parsed_ok = false` hoặc `validated = false` để phân loại ngay.

**M1.2 — Mock provider với deterministic output**

Implement `MockAgentModel` trả về response cố định từ file fixture:

```
fixtures/
  agents/
    creator/
      genesis_region.json        -- prompt context + expected response
      genesis_creature.json
    civilization/
      found_tribe.json
      expand_settlement.json
    storyteller/
      festival.json
      war_declaration.json
```

Mỗi fixture chứa:
```json
{
  "prompt_context": { "world_year": 50, "regions": ["reg_01"], "civs": [] },
  "llm_response": "{ \"type\": \"creation\", ... }",
  "expected_result": { "parsed": true, "validated": true, "canonical": true }
}
```

CI chạy toàn bộ fixtures qua pipeline thật (parse → Guardian → Historian) mà không gọi LLM.

**M1.3 — Snapshot testing cho world state**

Sau một chuỗi N ticks với mock provider:
- Dump world state thành JSON snapshot.
- So sánh với golden snapshot.
- Bất kỳ thay đổi nào ở parser, Guardian rules, hoặc Historian logic sẽ break snapshot → developer biết ngay impact.

**M1.4 — Error tagging theo layer**

Mọi error trong pipeline phải carry metadata:

```rust
enum PipelineStage {
    PromptBuild,
    LlmCall,
    JsonParse,
    GuardianValidate,
    HistorianCanonize,
    StateCommit,
}

struct PipelineError {
    stage: PipelineStage,
    tick_id: u64,
    agent: String,
    message: String,
    raw_context: Option<String>,  // prompt hoặc response gây lỗi
}
```

Log và metrics group theo `stage` → dashboard nhìn là biết layer nào đang có vấn đề.

**Khi nào implement:** Sprint 2 (cùng lúc với event pipeline). `llm_call_log` và `MockAgentModel` phải có trước khi gọi LLM thật ở Sprint 3.

---

### 2. Guardian & Historian là bottleneck kỹ thuật

**Vấn đề**

Mọi proposal đều phải qua Guardian validate → Historian canonize. Hiện tại:

- Guardian check: logic, duplication, progression rules, world boundaries ([AGENT-RUNTIME.md](AGENT-RUNTIME.md) §4 step 5).
- Historian: chọn notable events để đánh dấu canonical ([MVP-SPEC.md](MVP-SPEC.md) §3.1 item 4-5).

Mỗi event type mới (`creation`, `war`, `religion`, `trade`...) cần bộ rules riêng ở Guardian. Với 9 event types hiện tại trong [event-model.md](event-model.md), mỗi type cần 3–5 rules → ~40 rules cho V1. V2 thêm agents → thêm event types → rules nhân bản.

Nếu rules là hardcoded `if/else`, maintenance cost sẽ phi tuyến.

- Ref: [MVP-SPEC.md](MVP-SPEC.md) §3 (agents V1), [event-model.md](event-model.md) §1 (event types)

**Mitigation: Declarative Rule Engine + Composable Validators**

**M2.1 — Rules là data, không phải code**

Định nghĩa rules dạng declarative (TOML/JSON), mỗi event type có file riêng:

```
rules/
  creation.toml
  war.toml
  religion.toml
  migration.toml
  ...
```

Ví dụ `rules/war.toml`:
```toml
[meta]
event_type = "war"
version = 1

[[validators]]
name = "both_civs_exist"
check = "all_entities_exist"
fields = ["affected_entities.attacker_civ_id", "affected_entities.defender_civ_id"]

[[validators]]
name = "not_self_war"
check = "fields_not_equal"
fields = ["affected_entities.attacker_civ_id", "affected_entities.defender_civ_id"]

[[validators]]
name = "civs_in_contact"
check = "entities_share_region"
fields = ["affected_entities.attacker_civ_id", "affected_entities.defender_civ_id"]

[[validators]]
name = "no_duplicate_active_war"
check = "no_active_event_between"
params = { event_type = "war", lookback_years = 25 }
```

Guardian runtime đọc rules, apply lên proposal. Thêm event type = thêm file TOML, không sửa code Guardian.

**M2.2 — Validator composable pipeline**

Guardian không phải 1 function lớn, mà là pipeline of validators:

```rust
trait Validator {
    fn validate(&self, proposal: &EventProposal, world: &WorldState) -> ValidationResult;
}

// Built-in validators (reusable across event types):
struct AllEntitiesExist;
struct FieldsNotEqual;
struct EntitiesShareRegion;
struct NoActiveEventBetween;
struct WorldSizeCap;
struct TickEventCap;

// Guardian chạy:
fn guardian_validate(proposal, world, rules) -> Result<(), Vec<RuleViolation>> {
    let validators = rules.get(proposal.event_type);
    validators.iter().map(|v| v.validate(proposal, world)).collect()
}
```

Lợi ích:
- Mỗi validator test được độc lập.
- Thêm event type chỉ compose từ validators có sẵn.
- Validator mới viết 1 lần, dùng cho nhiều event types.

**M2.3 — Historian cũng declarative**

Thay vì hardcode "event nào là notable", dùng scoring:

```toml
[scoring]
# Base score theo event type
war = 80
religion = 60
creation = 50
trade = 30

[bonuses]
first_of_type_in_era = 20       # event type chưa từng xảy ra trong era hiện tại
involves_major_civ = 15          # civ có population > threshold
era_changing = 100               # khi event trigger era change

[thresholds]
canonical_min_score = 50
```

**M2.4 — Property-based testing cho rules**

Dùng proptest (Rust) hoặc tương đương:
- Generate random `EventProposal` → chạy qua Guardian → verify không panic.
- Generate proposal vi phạm 1 rule cụ thể → verify bị reject đúng rule.
- Generate N proposals liên tiếp → verify world state vẫn consistent.

**Khi nào implement:** Sprint 2 (Guardian/Historian pipeline). Bắt đầu với 3–4 validators cơ bản, thêm dần theo event type.

---

### 3. Monolithic service ghép quá nhiều trách nhiệm

**Vấn đề**

`ai-dreams-server` chứa 4 subsystems có lifecycle hoàn toàn khác nhau:

| Subsystem | Lifecycle | Failure impact |
|-----------|-----------|---------------|
| HTTP API | Request/response, stateless | User thấy error |
| Simulation scheduler | Long-running loop, stateful | World ngừng tiến hóa |
| LLM runtime | External I/O, latency 1–30s | Timeout, cost spike |
| SQLite | Synchronous I/O, single-writer | Toàn bộ app block |

Khi LLM provider timeout 30s, simulation loop block → HTTP API vẫn sống nhưng không có event mới → user nghĩ app chết. Khi debug tick loop, phải restart toàn bộ server → mất frontend state.

- Ref: [MVP-SPEC.md](MVP-SPEC.md) §4.2, [system-design.md](system-design.md) §2

**Mitigation: Process Modes + Internal Isolation**

Không cần tách thành microservices (quá sớm cho V1), nhưng cần **isolation nội bộ**.

**M3.1 — Process modes via CLI flag**

```bash
# Full mode (default) — tất cả chạy chung
ai-dreams-server

# API-only — chỉ HTTP, không chạy simulation (cho frontend dev)
ai-dreams-server --mode api-only

# Sim-only — chỉ simulation, không HTTP (cho debug tick)
ai-dreams-server --mode sim-only

# Single-tick — chạy đúng 1 tick rồi exit (cho testing)
ai-dreams-server --mode single-tick
```

Implement bằng feature flags trong `main()`:

```rust
match args.mode {
    Mode::Full => {
        spawn_api_server(db.clone());
        spawn_simulation_loop(db.clone(), llm.clone());
    }
    Mode::ApiOnly => {
        spawn_api_server(db.clone());
    }
    Mode::SimOnly => {
        spawn_simulation_loop(db.clone(), llm.clone());
    }
    Mode::SingleTick => {
        run_single_tick(db.clone(), llm.clone()).await;
    }
}
```

**M3.2 — Separate tokio task groups với supervision**

Trong full mode, mỗi subsystem chạy trong task group riêng:

```rust
let (api_handle, sim_handle) = tokio::join!(
    tokio::spawn(api_server(db.clone())),
    tokio::spawn(simulation_loop(db.clone(), llm.clone())),
);

// Nếu sim crash, API vẫn sống — user vẫn xem được data cũ
// Nếu API crash, sim vẫn chạy — world vẫn tiến hóa
```

**M3.3 — Simulation control qua channel, không shared mutable state**

```rust
enum SimCommand {
    Pause,
    Resume,
    Tick,              // manual single tick
    Shutdown,
}

// API handler gửi command:
async fn pause_handler(tx: Sender<SimCommand>) {
    tx.send(SimCommand::Pause).await;
}

// Sim loop nhận command:
loop {
    select! {
        cmd = rx.recv() => match cmd {
            SimCommand::Pause => { /* wait for Resume */ },
            SimCommand::Tick => { run_one_tick().await; },
            ...
        },
        _ = tick_interval.tick() => { run_one_tick().await; },
    }
}
```

Lợi ích:
- Pause/resume không cần restart server.
- Manual tick từ API handler không conflict với auto loop.
- Debug: pause sim, inspect DB, resume.

**M3.4 — LLM call isolation với timeout + circuit breaker**

```rust
async fn call_llm_with_protection(model: &dyn AgentModel, prompt: AgentPrompt) -> Result<AgentReply> {
    let result = tokio::time::timeout(
        Duration::from_secs(30),
        model.complete(prompt)
    ).await;

    match result {
        Ok(Ok(reply)) => Ok(reply),
        Ok(Err(e)) => {
            metrics::increment("llm.error");
            Err(e)
        }
        Err(_) => {
            metrics::increment("llm.timeout");
            // Tick này không có event, nhưng sim loop không crash
            Err(Error::LlmTimeout)
        }
    }
}
```

**Khi nào implement:** Sprint 0–1. Process modes và task separation nên có từ scaffold. Channel-based control ở Sprint 2.

---

### 4. Schema V1 rộng hơn mức cần thiết

**Vấn đề**

[IMPLEMENTATION-PLAN.md](IMPLEMENTATION-PLAN.md) Sprint 1 liệt kê 10 tables: `worlds`, `regions`, `locations`, `civilizations`, `settlements`, `creatures`, `events`, `religions`, `cultures`, `resources`, `eras`.

Nhưng [MVP-SPEC.md](MVP-SPEC.md) §2–3 cho thấy V1 usable path chỉ thực sự cần:
- `worlds`, `regions`, `civilizations`, `settlements`, `events` — cho Dream Feed + World Overview.
- `eras` — cho Timeline grouping.
- `locations` — cho Creator agent output.

Các tables `creatures`, `religions`, `cultures`, `resources` chỉ có agent tiêu thụ khi V2 agents (Culture, Myth, Ecology, Economy) được bật. Tạo sớm = schema churn khi domain model chưa ổn.

- Ref: [database-schema.md](database-schema.md), [world-model.md](world-model.md)

**Mitigation: Phased Schema + Soft References**

**M4.1 — Schema V1 core (Sprint 1)**

Chỉ tạo tables thực sự cần cho MVP:

```sql
-- Core tables (Sprint 1)
CREATE TABLE worlds ( ... );
CREATE TABLE regions ( ... );
CREATE TABLE locations ( ... );
CREATE TABLE civilizations ( ... );
CREATE TABLE settlements ( ... );
CREATE TABLE events ( ... );
CREATE TABLE eras ( ... );
```

**M4.2 — Soft references qua events JSON cho entities chưa có table**

Khi Creator agent tạo creature, hoặc Storyteller đề cập religion — chưa cần table riêng. Lưu trong `affected_entities` JSON:

```json
{
  "type": "creation",
  "description": "A dragon species emerges in the northern mountains",
  "affected_entities": {
    "region_id": "reg_01",
    "creature": { "name": "Storm Drake", "description": "..." }
  }
}
```

`creature` ở đây là unstructured data trong event. Khi V2 cần query creatures riêng → migrate: scan events, extract creatures → populate `creatures` table.

**M4.3 — Schema V2 extension (Sprint 7+)**

Khi Culture/Myth agents được bật:

```sql
-- V2 tables (Sprint 7+, khi agent tương ứng được implement)
CREATE TABLE creatures ( ... );
CREATE TABLE religions ( ... );
CREATE TABLE cultures ( ... );
CREATE TABLE resources ( ... );  -- Sprint 8, khi Economy agent lên
```

Migration script đọc từ events JSON → backfill tables.

**M4.4 — Schema version tracking**

```sql
CREATE TABLE schema_version (
    version     INTEGER PRIMARY KEY,
    applied_at  TEXT NOT NULL DEFAULT (datetime('now')),
    description TEXT NOT NULL
);

-- V1: version 1 — core tables
-- V2: version 2 — creatures, religions
-- V3: version 3 — cultures, resources
```

**Khi nào implement:** Sprint 1. Tạo 7 core tables thay vì 10. Còn lại defer.

---

## P2 — Important Limitations

### 5. Observability đến muộn so với nơi risk xuất hiện

**Vấn đề**

[PROJECT-MASTER-PLAN.md](PROJECT-MASTER-PLAN.md) §5 đặt metrics dashboard ở Sprint 11, nhưng KPIs cần đo (tick success rate, Guardian reject rate, token cost, tick duration) đã là risk từ Sprint 2–3 khi bắt đầu gọi LLM thật.

Không có observability ở Sprint 2–3 nghĩa là:
- Không biết 1 tick tốn bao nhiêu tokens / bao nhiêu tiền.
- Không biết Guardian reject bao nhiêu % proposals (và lý do gì).
- Không biết prompt context có phình quá mức không.
- Không phát hiện được LLM provider degradation.

**Mitigation: Minimal Observability từ Sprint 2**

**M5.1 — Structured tick log (không cần Grafana, chỉ cần structured output)**

Mỗi tick emit 1 structured log entry:

```json
{
  "tick_id": 42,
  "world_year": 210,
  "agents_selected": ["creator", "civilization"],
  "proposals_generated": 2,
  "proposals_accepted": 1,
  "proposals_rejected": 1,
  "reject_reasons": ["entity_not_found: civ_99"],
  "events_canonical": 1,
  "llm_calls": 2,
  "total_tokens_in": 1200,
  "total_tokens_out": 450,
  "total_latency_ms": 3400,
  "estimated_cost_usd": 0.0023,
  "tick_duration_ms": 4100
}
```

Ghi vào file `logs/tick-log.jsonl` hoặc bảng `tick_log` — chỉ cần `grep` hoặc `jq` để phân tích.

**M5.2 — CLI report command**

```bash
# Xem tổng quan 50 ticks gần nhất
ai-dreams-server report --last 50

# Output:
# Ticks: 50 | Success: 47 (94%) | Failed: 3
# Events generated: 89 | Canonical: 34
# Guardian reject rate: 12%
# Top reject reasons: entity_not_found (5), duplicate_event (3)
# Avg tick duration: 3.2s | Avg LLM latency: 2.1s
# Total tokens: 82,400 | Est. cost: $0.12
```

Không cần dashboard phức tạp — CLI report đủ cho solo/small team.

**M5.3 — Cost alarm đơn giản**

```rust
const COST_ALERT_PER_TICK: f64 = 0.01;  // $0.01/tick

if tick_cost > COST_ALERT_PER_TICK {
    warn!("Tick {} cost ${:.4} exceeds threshold", tick_id, tick_cost);
}
```

**Khi nào implement:** Sprint 2 (cùng lúc với tick pipeline). Đây chỉ là structured logging + 1 CLI command, effort rất nhỏ.

---

### 6. API contract intentionally mỏng

**Vấn đề**

[MVP-SPEC.md](MVP-SPEC.md) §4.1 chỉ liệt kê endpoint names, không định nghĩa response shape. Khi frontend (Sprint 4) và backend (Sprint 1–3) phát triển song song, projection shape sẽ drift.

Ví dụ: frontend expect `GET /worlds/current/events` trả envelope chuẩn kiểu `{ success, code, message, data: [...], meta: { total: N } }` nhưng backend trả `[...]` flat → runtime error ở Sprint 4.

**Mitigation: Lightweight Contract trước Sprint 4**

**M6.1 — Response type definitions (shared)**

Viết TypeScript types cho API responses (đây là contract, không phải OpenAPI spec nặng):

```typescript
// contracts/api-types.ts

interface ApiResponse<T> {
  success: boolean;
  code: string;     // 4-digit business code, e.g. "0000"
  message: string;
  data: T;
  meta?: {
    page?: number;
    page_size?: number;
    total?: number;
    filters?: Record<string, unknown>;
  };
  errors?: Array<{ field: string; reason: string }>;
}

interface WorldSummaryDto {
  world_id: string;
  name: string;
  current_year: number;
  current_era: { era_id: string; name: string } | null;
  stats: {
    regions: number;
    civilizations: number;
    settlements: number;
    canonical_events: number;
  };
  highlights: string[];
}

interface WorldEventDto {
  event_id: string;
  year: number;
  event_type: string;
  agent: string;
  description: string;
  affected_entities: Record<string, unknown>;
  is_canonical: boolean;
}

type WorldSummaryResponse = ApiResponse<WorldSummaryDto>;
type EventsResponse = ApiResponse<WorldEventDto[]>;

interface TimelineEraDto {
  era_id: string;
  name: string;
  start_year: number;
  end_year: number | null;
  summary: string | null;
  major_events_count: number;
}
```

**M6.2 — Contract test**

Backend test: serialize actual response → validate against contract types.

```rust
#[test]
fn events_response_matches_contract() {
    let response = get_events(world_id, None, None);
    let json: serde_json::Value = serde_json::to_value(&response).unwrap();

    // Verify shape
    assert!(json["success"].is_boolean());
    assert!(json["code"].is_string());
    assert!(json["message"].is_string());
    assert!(json["data"].is_array());
    assert!(json["meta"]["total"].is_number());
    for event in json["data"].as_array().unwrap() {
        assert!(event["event_id"].is_string());
        assert!(event["year"].is_number());
        assert!(event["event_type"].is_string());
        assert!(event["description"].is_string());
    }
}
```

**Khi nào implement:** Cuối Sprint 3 (trước khi frontend bắt đầu ở Sprint 4). Effort: 1–2 ngày.

---

### 7. SQLite + 1 world + single process

**Vấn đề**

Limitation chủ đích, nhưng gây khó khăn khi dev muốn:
- So sánh 2 world chạy cùng điều kiện khác nhau.
- Replay 1 world từ snapshot cũ.
- Test long-run behavior (500+ ticks).

**Mitigation: Database-per-world + Snapshot**

**M7.1 — Database file = world identity**

Thay vì 1 file `ai-dreams.db` chứa tất cả, mỗi world là 1 file:

```
data/
  world-alpha.db
  world-beta.db
  world-gamma.db
```

Config:
```bash
AI_DREAMS_WORLD_DB=data/world-alpha.db
```

Vẫn là single-process, single-world runtime. Nhưng:
- Copy file = clone world.
- Đổi env = switch world.
- Multiple instances có thể chạy song song trên các port khác nhau.

**M7.2 — World snapshot (cp đủ)**

```bash
# Snapshot trước khi thử God Mode
cp data/world-alpha.db data/snapshots/world-alpha-year-500.db

# Nếu God Mode phá world → restore
cp data/snapshots/world-alpha-year-500.db data/world-alpha.db
```

Đơn giản, zero code, tận dụng SQLite là single file.

**M7.3 — Replay mode**

Kết hợp với M1.1 (`llm_call_log`):

```bash
# Replay world từ tick 0 đến tick 100, dùng recorded LLM responses
ai-dreams-server --mode replay --from-tick 0 --to-tick 100 --source data/snapshots/world-alpha-year-0.db
```

**Khi nào implement:** M7.1 ở Sprint 1 (chỉ là đổi cách đặt tên DB file). M7.2 miễn phí (cp). M7.3 ở Sprint 3+.

---

### 8. Delivery plan tham vọng vs. docs-only status

**Vấn đề**

Execution horizon hiện tại đã mở tới 20 sprints. MVP gate vẫn ở Sprint 6 (= khoảng 3 tháng), Platform Expansion gate ở Sprint 12 (= khoảng 6 tháng), và Community Vision gate ở Sprint 20 (= khoảng 10 tháng) nếu giữ cadence 2 tuần/sprint. Repo hiện tại chưa có dòng code nào.

Nếu solo hoặc 2 người, Sprint 0–2 dễ bị kéo dài vì:
- Rust learning curve (nếu chưa quen).
- LLM integration luôn có surprises.
- Schema + domain model cần iterate.

**Mitigation: Vertical Slice Priority + Flexible Sprint Length**

**M8.1 — Sprint length thực tế**

Chấp nhận 3–4 tuần/sprint cho solo dev, như [IMPLEMENTATION-PLAN.md](IMPLEMENTATION-PLAN.md) §1 đã note. Không ép 2 tuần nếu capacity không đủ.

**M8.2 — Vertical slice over horizontal layer**

Thay vì Sprint 1 = toàn bộ schema, Sprint 2 = toàn bộ pipeline:

```
Sprint 1: world + regions + 1 event type (creation) → manual tick → 1 event in DB
Sprint 2: + civilizations + settlements + Guardian basic → 3 event types working
Sprint 3: + LLM real → Genesis mode → Dream Feed API
```

Mỗi sprint có output chạy được end-to-end, chỉ scope hẹp hơn.

**M8.3 — Sớm chốt "Walking Skeleton"**

Sprint 0 phải ra được:
```
cargo run → server start → POST /tick → mock event in DB → GET /events → JSON response
npm run dev → UI shows event list from API
```

Đây là walking skeleton: toàn bộ layers connected nhưng mỗi layer chỉ ở mức stub. Từ đây iterate thêm depth.

---

## Tổng hợp Mitigation Roadmap

| Sprint | Mitigations cần có |
|--------|-------------------|
| **Sprint 0** | M3.1 (process modes), M8.3 (walking skeleton) |
| **Sprint 1** | M4.1 (slim schema 7 tables), M7.1 (db-per-world naming) |
| **Sprint 2** | M1.1 (llm_call_log), M1.2 (mock provider + fixtures), M1.4 (error tagging), M2.1–M2.2 (declarative rules + composable validators), M3.2–M3.3 (task isolation + channels), M5.1–M5.2 (structured tick log + CLI report) |
| **Sprint 3** | M1.3 (snapshot testing), M6.1–M6.2 (API contract + test), M7.3 (replay mode) |
| **Sprint 7+** | M4.3 (V2 schema extension) |

---

## Đánh giá tổng thể

**Chấp nhận được cho V1:** 1 world, SQLite, single binary, 1 LLM provider, không map/graph.

**Phải xử lý trước Sprint 3:**
1. Mock provider + record/replay (nếu không, Sprint 3 gọi LLM thật sẽ blind debugging).
2. Declarative Guardian rules (nếu không, mỗi event type mới = spaghetti code).
3. Process modes + sim control channels (nếu không, dev experience sẽ rất frustrating).
4. Structured tick logging (nếu không, cost và quality đều invisible).
5. Slim schema (nếu không, migration churn khi domain model chưa stable).
6. API contract types (nếu không, frontend sẽ build trên assumptions sai).

---

## 4 Mitigation nên ưu tiên trước khi code sâu hơn

Day la 4 viec nen khoa som nhat de tranh lao vao implementation sau roi moi xu ly nen tang. Muc tieu cua section nay khong phai lap lai toan bo risk analysis o tren, ma la rut ra 4 workstream can lam truoc khi team code sau vao simulation loop, frontend projections, va agent runtime.

### A. Keo minimal observability tu phase muon ve Sprint 2-3

Ly do:

- Risk that su xuat hien ngay khi co tick pipeline that va LLM calls.
- Neu khong co observability som, team se khong biet:
  - tick nao fail
  - fail o layer nao
  - provider latency/tokens/cost ra sao
  - Guardian dang reject vi ly do gi

Can co toi thieu:

- `tick_log` hoac `logs/tick-log.jsonl` cho moi tick.
- `llm_call_log` cho moi lan goi provider.
- log fields bat buoc:
  - `tick_id`
  - `agents_selected`
  - `proposals_generated`
  - `proposals_accepted`
  - `proposals_rejected`
  - `reject_reasons`
  - `latency_ms`
  - `tokens_in`
  - `tokens_out`
  - `estimated_cost_usd`
- 1 lenh `report --last N` de tong hop success rate, reject rate, avg latency, token cost.

Definition of done:

- chay 20-50 ticks mock va xem duoc top reject reasons
- phan biet duoc loi `JsonParse`, `GuardianValidate`, `HistorianCanonize`, `StateCommit`
- co cost-per-tick de chot threshold canh bao

Ref lien quan:

- M1.1, M1.4
- M5.1, M5.2, M5.3

### B. Tao deterministic simulation harness truoc khi goi LLM that

Ly do:

- Neu khong co harness, moi bug trong tick pipeline se tro thanh bug "co luc co, co luc khong".
- Day la limitation nghiem trong nhat cua he thong vi pipeline co LLM text -> parse -> validate -> canonize.

Can co toi thieu:

- `MockAgentModel`
- fixture library theo agent
- replay path bo qua live LLM
- golden snapshot cho world state sau N ticks

Deliverables can co:

- `fixtures/agents/...`
- world seed snapshot ban dau
- replay lenh kieu:
  - `--mode single-tick`
  - `--mode replay --from-tick X --to-tick Y`
- contract test cho parser -> Guardian -> Historian

Definition of done:

- co it nhat 1 genesis path chay deterministic end-to-end
- cung 1 fixture sequence thi world snapshot luon giong nhau
- khi doi Guardian rule hoac Historian threshold, snapshot drift se lo ra ngay trong CI

Ref lien quan:

- M1.1, M1.2, M1.3
- M7.3

### C. Rut gon schema V1 ve entity that su can cho MVP path

Ly do:

- Domain model hien nay de bi over-modeling qua som.
- Neu team tao het `creatures`, `religions`, `cultures`, `resources` ngay Sprint 1, migration churn se rat cao trong khi runtime chua on dinh.

Schema V1 nen khoa o muc core:

- `worlds`
- `regions`
- `locations`
- `civilizations`
- `settlements`
- `events`
- `eras`

Phan con lai:

- dua vao `affected_entities` JSON trong `events`
- chi tach ra table rieng khi V2 agents that su duoc bat

Definition of done:

- world overview va dream feed chay duoc chi voi 7 core tables
- Creator/Civilization/Storyteller co du data model de hoat dong
- co migration plan ro rang cho `creatures`, `religions`, `cultures`, `resources` ve sau

Ref lien quan:

- M4.1, M4.2, M4.3, M4.4

### D. Viet contract ro cho `GET /worlds/current`, `GET /worlds/current/events`, va projections timeline/feed truoc khi frontend di xa

Ly do:

- Frontend drift thuong khong den tu endpoint khong ton tai, ma den tu response shape va projection shape thay doi ngau hung.
- Neu khong khoa contract som, Sprint 4+ se ton effort vo ich de chase backend assumptions.

Can khoa som:

- response envelope thong nhat
- world summary shape
- event list shape
- `meta`/paging shape
- empty state behavior
- filter behavior
- timeline projection shape cho era grouping va major events

Deliverables can co:

- `API-CONTRACT.md`
- `API-CODES.md`
- shared DTO/type contract
- contract tests cho backend serializers

Definition of done:

- frontend co the scaffold Dream Feed va World Overview ma khong can doan shape
- backend test fail ngay neu response drift
- pagination/filter/empty-state da duoc chot bang contract, khong con implicit assumptions

Ref lien quan:

- M6.1, M6.2
- `API-CONTRACT.md`
- `API-CODES.md`

### Thu tu uu tien de lam

Neu can xep theo critical path thuc te, thu tu nen la:

1. Deterministic simulation harness
2. Minimal observability
3. Slim schema V1
4. API/projection contract

Ly do:

- Harness + observability giai quyet kha nang debug va phan loai loi som.
- Slim schema giu cho data model khong vo to qua som.
- API contract khoa interface giua backend va frontend truoc khi UI consume du lieu that.

### Mapping ngan theo sprint

| Sprint | Viec can khoa |
| --- | --- |
| `Sprint 1` | Slim schema V1 + DB-per-world naming |
| `Sprint 2` | Mock provider, fixtures, `llm_call_log`, structured tick log, error tagging |
| `Sprint 3` | Snapshot replay, API contract tests, timeline/feed projection contract |

Ket luan:

- Neu 4 workstream nay duoc khoa som, team co the code sau vao simulation va UI ma van giu duoc kha nang debug, replay, va thay doi an toan.
- Neu bo qua, moi feature moi se lam tang do mo ho cua he thong nhanh hon toc do team co the kiem soat.
