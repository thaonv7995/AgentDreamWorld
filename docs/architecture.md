# System Architecture – AI Dreams World

AI Dreams World được tổ chức thành 4 layer chính:

1. **Dream Engine** (core simulation)
2. **Agent Layer** (multi-agent AI)
3. **World Model** (persistent world state)
4. **Visualization Layer** (UI khám phá thế giới)

---

## 1. Dream Engine

Dream Engine là orchestrator trung tâm, chịu trách nhiệm:

- Lên lịch tick simulation (Genesis + Evolution).
- Chọn agents hoạt động trong mỗi tick.
- Build context (world/era/region summary + recent events).
- Gọi Agent Runtime (LLM) để nhận Event Proposals.
- Gọi Guardian để validate.
- Commit world updates & notify Historian.

High-level flow mỗi tick:

1. Chọn agent(s) theo scheduler.
2. Lấy world snapshot + recent canonical events.
3. Build `AgentPrompt` cho từng agent.
4. Gọi LLM thông qua abstraction `AgentModel` (có timeout + circuit breaker).
5. Parse output thành `EventProposal`.
6. **Log LLM call** vào `llm_call_log` (prompt, response, latency, tokens) — cho record/replay.
7. Guardian validate qua **declarative rule engine** → World Model update.
8. Historian thêm event vào canonical timeline.
9. Emit **structured tick log** (metrics, reject reasons, cost).

---

## 2. Agent Layer

Agent Layer chứa các **AI agents chuyên biệt**, chia thành hai nhóm:

**V1 Core Agents (Sprint 1–3):**

- Creator Agent – tạo locations, primitive creatures, anomalies.
- Civilization Agent – phát triển tribes → villages → towns → kingdoms → empires.
- Storyteller Agent – sinh narrative events, festivals, discoveries, diplomacy.
- Historian Agent – chọn event canonical, viết era summaries.
- Guardian Agent – coherence & conflict resolution qua **declarative rule engine**.

**V2+ Extended Agents (Sprint 7+):**

- Culture Agent – phong tục, lễ hội, biểu tượng.
- Myth Agent – thần, truyền thuyết, lời tiên tri.
- Ecology Agent – climate, ecosystem, resource distribution.
- Economy Agent – trade routes, currencies, scarcity.
- Chaos Agent – thảm họa, anomaly, mutations.

Agents **không giữ state lâu dài**; mọi state của thế giới nằm ở World Model.

### 2.1. Guardian Rule Engine

Guardian không hardcode rules, mà đọc từ **declarative rule files** (TOML) per event type:

```
rules/
  creation.toml
  war.toml
  religion.toml
  ...
```

Mỗi rule file định nghĩa danh sách validators composable (`all_entities_exist`, `fields_not_equal`, `no_duplicate_active_war`...). Thêm event type = thêm file, không sửa code Guardian.

Chi tiết: xem [LIMITATIONS.md](LIMITATIONS.md) §M2.1–M2.2.

---

## 3. World Model

World Model là đại diện có cấu trúc của thế giới, lưu trong DB (V1: SQLite, optional Postgres).

### 3.1. Phased Schema

**V1 Core Tables (Sprint 1):** — chỉ tạo tables thực sự cần cho MVP path.

- World, Region, Location.
- Civilization, Settlement.
- Event, Era.

**V2+ Extension Tables (Sprint 7+):** — tạo khi agent tương ứng được implement.

- Creature, Religion, Culture, Resource.

Trước khi có table riêng, entities phụ được lưu dạng **soft references** trong `affected_entities` JSON của events. Khi V2 cần query riêng → migration script extract từ events → backfill tables.

### 3.2. Event Sourcing

Mọi thay đổi thế giới đi qua **event-sourcing**:

- Bảng `events` append-only.
- World snapshot có thể được dựng lại từ event log.
- Historian đánh dấu subset events là canonical/notable.

### 3.3. Database-per-world

Mỗi world là một SQLite file riêng (`data/world-{name}.db`). Copy file = clone world, đổi env = switch world. Hỗ trợ snapshot/restore bằng `cp`.

Chi tiết: xem [LIMITATIONS.md](LIMITATIONS.md) §M4, §M7.

---

## 4. Visualization Layer

Visualization Layer là frontend (React + Vite) dùng để quan sát thế giới.

Các component chính:

- Dream Feed – stream event.
- Timeline Explorer – trục thời gian.
- World Overview – danh sách regions/civilizations.
- (Phase 2+) Civilization Viewer, Map, Mythology Browser, Knowledge Graph.

Visual design phân tầng:

- Structural UI (layout, text, icons) – luôn có, không cần AI image.
- Symbolic assets (sigils, icons) – procedural/static.
- Narrative art (AI image optional) – enrich content.

---

## 5. High-level Data & Control Flow

```text
User UI  →  HTTP API (backend)
              ↓
         Dream Engine
              ↓
         Agent Runtime  →  LLM Provider(s)
              ↓
           Guardian
              ↓
          World Model  ← Historian
              ↑
        Visualization Layer đọc world state/events
```

---

## 6. Deployment View (V1)

- Một binary backend `ai-dreams-server` (Rust):
  - HTTP API.
  - Simulation loop.
  - LLM client(s).
  - SQLite file.
- Một frontend SPA (React) được serve bởi backend (single binary mode) hoặc chạy dev riêng.

### 6.1. Process Modes

Backend hỗ trợ nhiều modes qua CLI flag để tách biệt subsystems khi dev/debug:

```bash
ai-dreams-server                    # Full mode (default) — API + simulation
ai-dreams-server --mode api-only    # Chỉ HTTP, không chạy simulation (frontend dev)
ai-dreams-server --mode sim-only    # Chỉ simulation, không HTTP (debug tick)
ai-dreams-server --mode single-tick # Chạy đúng 1 tick rồi exit (testing)
```

### 6.2. Internal Isolation

Trong full mode, HTTP API và simulation loop chạy trong tokio task groups riêng biệt. Simulation control (pause/resume/tick) đi qua channel, không shared mutable state. LLM calls có timeout + circuit breaker để không block toàn bộ app.

Chi tiết: xem [LIMITATIONS.md](LIMITATIONS.md) §M3.

### 6.3. Observability (từ Sprint 2)

Mỗi tick emit structured log entry (JSONL) gồm: tick_id, agents, proposals accepted/rejected, reject reasons, token count, latency, estimated cost. CLI report command (`ai-dreams-server report`) tổng hợp metrics từ tick log.

Chi tiết: xem [LIMITATIONS.md](LIMITATIONS.md) §M5.

Optional (V2+):

- Postgres/Redis profile cho scale lớn.
- Metrics dashboard (Grafana/Prometheus).
