# AI Dreams World – Implementation Plan

Tài liệu này chuyển bộ product/spec docs hiện có thành **kế hoạch triển khai thực thi** theo phase và sprint.

Mục tiêu:

- Biến roadmap hiện tại thành execution plan có thể giao việc.
- Giữ scope V1 không trượt khỏi `MVP-SPEC.md`.
- Cho team biết mỗi sprint phải làm tính năng gì, ra deliverable gì, và khi nào được coi là xong.

Checklist chi tiết theo từng sprint và theo role nằm trong `docs/sprints/README.md`.
Backlog điều phối cấp delivery nằm trong `docs/sprints/MASTER-BACKLOG.md`.

---

## 1. Planning Assumptions

- Baseline cadence: **2 tuần / sprint**.
- Snapshot repo hiện tại là **docs-only**, nên kế hoạch bắt đầu bằng việc scaffold codebase.
- Mốc chốt:
  - **MVP gate** ở cuối **Sprint 6**
  - **Expanded Simulation gate** ở cuối **Sprint 8**
  - **Visualization gate** ở cuối **Sprint 10**
  - **Platform Expansion gate** ở cuối **Sprint 12**
- V1 phải luôn ưu tiên:
  - `SQLite embedded`
  - 1 world
  - 3 creative agents active/tick tối đa
  - Dream Feed + Timeline + World Overview
  - export wiki/annals cơ bản

Nếu team nhỏ hoặc solo, có thể giữ nguyên thứ tự sprint nhưng kéo dài mỗi sprint thành 3–4 tuần.

---

## 2. Workstreams Chính

| Workstream | Mục tiêu | Output chính |
| --- | --- | --- |
| Product & Scope | Giữ đúng MVP, tránh scope creep | backlog, acceptance criteria, release scope |
| Backend Core | Dream Engine, API, persistence | Rust server, DB schema, endpoints |
| Agent Runtime | Agent orchestration, model abstraction, validation | AgentModel, prompts, Guardian, Historian |
| Frontend | Quan sát thế giới và điều khiển tối thiểu | Dream Feed, Timeline, World Overview |
| Export & Content | Biến world thành content usable | wiki export, annals export |
| DevEx / Quality | Giảm friction, giữ chất lượng | scripts, CI, logging, test, packaging |

---

## 3. Phase Overview

| Phase | Sprint | Goal | Kết quả mong đợi |
| --- | --- | --- | --- |
| Phase 0 | Sprint 0 | Scaffold repo và execution rails | Repo runnable skeleton |
| Phase 1 | Sprint 1–2 | Core engine foundation | World model, SQLite, tick pipeline |
| Phase 2 | Sprint 3–4 | MVP vertical slice | Genesis + Dream Feed + World Overview |
| Phase 3 | Sprint 5–6 | MVP release candidate | Timeline + export + single-binary |
| Phase 4 | Sprint 7–8 | Expanded simulation | Culture/Myth/Ecology/Economy/Chaos |
| Phase 5 | Sprint 9–10 | Visualization expansion | Map, Civilization Viewer, Mythology, Graph |
| Phase 6 | Sprint 11–12 | Platform expansion | Optional advanced infra + multi-world foundation |

---

## 4. Detailed Sprint Plan

## Phase 0 – Project Foundation

### Sprint 0 – Repo Scaffold & Delivery Rails

**Goal**

Biến repo từ `docs-only` thành một codebase có thể khởi động được ở mức skeleton, bao gồm process modes và walking skeleton.

**Features**

- Tạo Rust workspace + `crates/server`.
- Tạo `frontend` React + Vite app.
- Tạo `.env.example` và config loading tối thiểu (bao gồm `AI_DREAMS_WORLD_DB`).
- Tạo `scripts/dev.sh` cho luồng dev cơ bản.
- Thiết lập lint/build scripts tối thiểu.
- Thiết lập project structure theo `ai-dreams-technical.md`.
- **Process modes** (`--mode full/api-only/sim-only/single-tick`) — xem [LIMITATIONS.md](LIMITATIONS.md) §M3.1.
- **Tokio task group separation** cho HTTP và simulation (stub) — xem [LIMITATIONS.md](LIMITATIONS.md) §M3.2.
- **Walking skeleton**: POST /tick (stub) → event in DB → GET /events → JSON → UI render.

**Deliverables**

- Backend stub chạy được, với process modes.
- Frontend shell chạy được.
- Walking skeleton: end-to-end stub flow.
- README + DEV-SETUP chuyển từ target-state sang runnable setup bước đầu.

**Exit Criteria**

- `cargo run --bin ai-dreams-server` trả về stub API.
- `cargo run --bin ai-dreams-server -- --mode api-only` chạy được.
- `npm run dev` mở được app shell.
- Walking skeleton: POST /tick → event in DB → GET /events → UI render.
- Contributor mới clone repo và chạy được skeleton trong < 30 phút.

---

## Phase 1 – Core Engine Foundation

### Sprint 1 – World Model, SQLite Schema, Persistence

**Goal**

Chốt domain model và persistence layer cho V1.

**Features**

- Implement schema SQLite cho **7 core tables** (slim schema — xem [LIMITATIONS.md](LIMITATIONS.md) §M4):
  - `worlds`
  - `regions`
  - `locations`
  - `civilizations`
  - `settlements`
  - `events`
  - `eras`
- **Defer** `religions`, `cultures`, `resources`, `creatures` sang Sprint 7+ (dùng soft references trong `events.affected_entities` JSON trước đó).
- Tạo migration/initialization flow với **schema version tracking**.
- Database-per-world: `data/world-{name}.db`.
- Implement repository/storage layer cơ bản.
- Tạo world bootstrap không dùng LLM để test persistence.

**Deliverables**

- DB init thành công khi app start.
- `GET /worlds/current` trả về world summary stub có dữ liệu thật.
- World seed đầu tiên persist được xuống SQLite.

**Exit Criteria**

- Có thể tạo world rỗng hoặc world seed và đọc lại sau restart.
- Vocabulary canon `Region` và `Settlement` được phản ánh trong schema và API.

### Sprint 2 – Event Pipeline, Tick Runner, Guardian/Historian, Observability

**Goal**

Có simulation loop tối thiểu chạy end-to-end bằng mock logic, với đầy đủ observability và test harness.

**Features**

- Implement `EventProposal` model.
- Append-only event log.
- Tick orchestrator với **channel-based simulation control** (`SimCommand`) — xem [LIMITATIONS.md](LIMITATIONS.md) §M3.3.
- `AgentModel` abstraction + **`MockAgentModel`** với fixture files — xem [LIMITATIONS.md](LIMITATIONS.md) §M1.2.
- Guardian **declarative rule engine** (TOML rules per event type, composable validators) — xem [LIMITATIONS.md](LIMITATIONS.md) §M2.1–M2.2.
- Historian **scoring-based canonicalization** — xem [LIMITATIONS.md](LIMITATIONS.md) §M2.3.
- `POST /worlds/current/tick` cho dev/debug.
- **`llm_call_log`** table: record/replay mọi LLM call — xem [LIMITATIONS.md](LIMITATIONS.md) §M1.1.
- **`tick_log`** table + structured tick logging — xem [LIMITATIONS.md](LIMITATIONS.md) §M5.1.
- **CLI report** (`ai-dreams-server report`) — xem [LIMITATIONS.md](LIMITATIONS.md) §M5.2.
- **Error classification** (`PipelineStage` tagging) — xem [LIMITATIONS.md](LIMITATIONS.md) §M1.4.
- **LLM timeout** (30s) + circuit breaker — xem [LIMITATIONS.md](LIMITATIONS.md) §M3.4.

**Deliverables**

- Một tick có thể sinh event, validate, commit vào world state.
- Phân biệt được raw events và canonical events.
- `llm_call_log` ghi mọi call, `tick_log` ghi metrics mỗi tick.
- CLI report tổng hợp được metrics.
- Mock provider chạy deterministic tick sequence.

**Exit Criteria**

- Manual tick tạo ra event hợp lệ.
- Guardian reject được event sai ID/progression cơ bản — bằng declarative rules, không hardcode.
- Historian đánh dấu được event canonical — bằng scoring, không hardcode.
- `ai-dreams-server report --last 10` hiển thị metrics đúng.
- Mock fixtures chạy qua pipeline thật thành công.

---

## Phase 2 – MVP Vertical Slice

### Sprint 3 – Genesis Mode & 3 Creative Agents V1

**Goal**

Có thế giới sinh ra từ hư không với 3 creative agents V1, kèm API contract rõ cho frontend.

**Features**

- Creator Agent V1.
- Civilization Agent V1.
- Storyteller Agent V1.
- Genesis mode 50–200 ticks.
- Config simulation boundaries:
  - world size
  - active agents/tick
  - event caps
- Event listing/filter API.
- **API contract types** (TypeScript): `WorldSummary`, `WorldEvent`, `EventsResponse`, `TimelineEra` — xem [LIMITATIONS.md](LIMITATIONS.md) §M6.1.
- **Contract tests** cho API responses — xem [LIMITATIONS.md](LIMITATIONS.md) §M6.2.
- **Snapshot testing**: golden world state sau mock genesis — xem [LIMITATIONS.md](LIMITATIONS.md) §M1.3.

**Deliverables**

- World đầu tiên có 3–4 regions.
- Có civilizations/settlements đầu tiên.
- Event feed data đọc được từ API.
- API contract types + tests sẵn sàng cho frontend Sprint 4.

**Exit Criteria**

- Sau genesis, world không còn là state rỗng.
- API event list trả về event có filter theo year/type/agent/civilization.
- API responses match contract types (contract tests pass).
- Snapshot test pass cho mock genesis.

### Sprint 4 – Dream Feed & World Overview UI

**Goal**

Người dùng bắt đầu quan sát được world chạy qua UI.

**Features**

- Frontend app shell.
- Dream Feed UI.
- World Overview UI.
- Filter theo year / event type / agent / civilization.
- Polling hoặc refresh flow đơn giản cho event stream.

**Deliverables**

- Trang chính xem được event feed.
- Panel/tabs xem regions, civilizations, settlements, summary.

**Exit Criteria**

- User mở app và thấy history hình thành theo thời gian.
- UI consume được API thật, không chỉ mock data.

---

## Phase 3 – MVP Release Candidate

### Sprint 5 – Timeline, Simulation Controls, God Mode Lite

**Goal**

Hoàn thiện trải nghiệm khám phá lịch sử của V1.

**Features**

- Timeline View.
- Zoom theo range cơ bản.
- Endpoint/control để pause/resume/manual tick.
- God Mode lite:
  - meteor
  - new region
  - magical anomaly
- Better summaries cho world/era/civilization.

**Deliverables**

- Timeline screen usable.
- God Mode preset hoạt động ở mức tối thiểu.

**Exit Criteria**

- User có thể tua lại history qua timeline.
- God Mode trigger tạo event hợp lệ và để lại hậu quả trong world state.

### Sprint 6 – Export, Single-Binary Mode, MVP Hardening

**Goal**

Đưa V1 tới mức có thể demo/release như một MVP hoàn chỉnh.

**Features**

- Export wiki.
- Export annals.
- Single-binary mode backend serve static frontend.
- Logging, error handling, config cleanup.
- QA pass theo Definition of Done của `MVP-SPEC.md`.
- Basic packaging/release notes.

**Deliverables**

- `/export/wiki` và `/export/annals` usable.
- Build release chạy được theo mode single-binary.
- MVP release candidate.

**Exit Criteria**

- Thỏa `Definition of Done` trong `MVP-SPEC.md`.
- Sau 5–10 phút chạy, Dream Feed + Timeline có history rõ ràng.
- Export tạo file readable.

---

## Phase 4 – Expanded Simulation

### Sprint 7 – Culture, Myth, Era Summaries

**Goal**

Bắt đầu làm cho thế giới có bản sắc văn hóa và thần thoại rõ ràng hơn.

**Features**

- Culture Agent.
- Myth Agent.
- Era summary generation.
- Canon compression/context summaries.
- Mythology data projection cơ bản.

**Deliverables**

- Myths/cults/customs bắt đầu xuất hiện trong history.
- Era summaries dùng được làm agent context.

**Exit Criteria**

- Agent context không cần đọc toàn bộ event log.
- World có output rõ về custom/myth ngoài war/discovery thông thường.

### Sprint 8 – Ecology, Economy, Chaos, Deeper Macro Rules

**Goal**

Mở rộng V2 simulation theo hướng macro nhưng vẫn giữ coherence.

**Features**

- Ecology Agent.
- Economy Agent.
- Chaos Agent.
- Trade/scarcity/conflict rules cơ bản.
- Collapse / famine / anomaly propagation rules.
- Balancing & simulation tuning.

**Deliverables**

- Event variety cao hơn nhưng không phá world coherence.
- Trade, scarcity, ecology bắt đầu tạo hậu quả liên hoàn.

**Exit Criteria**

- Invalid event rate giữ trong ngưỡng kiểm soát được.
- Guardian rules mở rộng đủ để ngăn V2 scope làm loạn canonical timeline.

---

## Phase 5 – Visualization Expansion

### Sprint 9 – Region Map & Civilization Viewer

**Goal**

Nâng từ text-first exploration sang exploration trực quan hơn.

**Features**

- Region/world map beta.
- Territory ownership projection.
- Civilization Viewer.
- Settlement distribution view.

**Deliverables**

- User xem được geography, ownership, civilization detail.

**Exit Criteria**

- Map và civilization detail dùng dữ liệu thật từ world model.
- Không hard-code layout theo từng world.

### Sprint 10 – Mythology Browser & Knowledge Graph

**Goal**

Biến world thành hệ thống lore có thể khám phá theo nhiều góc nhìn.

**Features**

- Mythology Browser.
- Knowledge Graph beta.
- Link entities:
  - civilization ↔ religion
  - myth ↔ event
  - war ↔ region/settlement
- Richer export artifacts.

**Deliverables**

- Người dùng khám phá lore bằng graph/browser, không chỉ qua timeline.

**Exit Criteria**

- Graph view usable cho ít nhất world V1/V2 size.
- Export giữ được các mối liên kết chính giữa entities.

---

## Phase 6 – Platform Expansion

### Sprint 11 – Optional Advanced Infra & Observability

**Goal**

Chuẩn bị project cho scale và contributor profile nâng cao.

**Features**

- Optional Postgres profile.
- Optional Redis/background jobs profile.
- Metrics dashboard:
  - tick duration
  - token cost/tick
  - Guardian reject rate
  - export success rate
- Perf/load pass cơ bản.

**Deliverables**

- Advanced profile chạy được như lựa chọn, không thay thế default SQLite mode.
- Quan sát được chi phí và sức khỏe simulation runtime.

**Exit Criteria**

- SQLite vẫn là default path.
- Advanced profile không làm vỡ MVP path.

### Sprint 12 – Multi-world Foundation & Project Ops

**Goal**

Mở nền cho roadmap Phase 5 mà chưa đòi full community feature.

**Features**

- Multi-world metadata model.
- World snapshot/fork foundation.
- World gallery metadata cơ bản.
- Project admin tools cho backup/restore/manage worlds.

**Deliverables**

- Có khả năng giữ nhiều world trong cùng hệ thống.
- Có đường mở cho alternate timeline/forking.

**Exit Criteria**

- World lifecycle không còn assume “single world forever” ở tầng data model.
- Không phá backward compatibility với current-world UX.

---

## 5. Phase Gates

| Gate | Cuối sprint | Điều kiện để qua gate |
| --- | --- | --- |
| Gate A – Scaffold Ready | Sprint 0 | Repo có backend/frontend skeleton chạy được |
| Gate B – Engine Foundation Ready | Sprint 2 | SQLite + event pipeline + manual tick hoạt động |
| Gate C – MVP Vertical Slice Ready | Sprint 4 | Genesis + Dream Feed + World Overview usable |
| Gate D – MVP Release Candidate | Sprint 6 | Timeline + export + single-binary + DoD V1 |
| Gate E – Expanded Simulation Ready | Sprint 8 | 10-agent catalog được mở dần với era summaries |
| Gate F – Visualization Ready | Sprint 10 | Map + Civilization Viewer + Mythology/Graph usable |
| Gate G – Platform Expansion Ready | Sprint 12 | Optional advanced infra + multi-world foundation |

---

## 6. Scope Control Rules

- Trước khi qua **Gate D**, không kéo các feature V2/V3 vào sprint nếu không trực tiếp unblock MVP.
- Mỗi sprint chỉ nên có:
  - 1 goal chính
  - 1 vertical slice rõ
  - 1–2 deliverable có thể demo
- Bất kỳ thay đổi scope nào làm trượt gate phải được cập nhật đồng thời ở:
  - `MVP-SPEC.md` nếu scope V1 đổi
  - `roadmap.md` nếu roadmap horizon đổi
  - `PROJECT-MASTER-PLAN.md` để cập nhật milestone và risk

---

## 7. Suggested Demo Rhythm

- Cuối mỗi sprint phải demo được ít nhất một trong các nhóm sau:
  - simulation runtime
  - API capability
  - UI capability
  - export/content capability
- Nếu sprint không demo được gì nhìn thấy được, coi như sprint đó chưa đóng đúng chất lượng.
