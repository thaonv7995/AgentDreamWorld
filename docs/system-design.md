# System Design – AI Dreams World

AI Dreams World là một hệ thống multi-agent simulation tạo ra và phát triển các thế giới hư cấu.

---

## 1. Core Components

1. Dream Engine (simulation orchestrator).
2. Agent Runtime & LLM integration.
3. World State Database (SQLite/Postgres).
4. Event Processing & Historian.
5. Visualization API (REST/WS) + Frontend UI.

---

## 2. Architecture Overview

```text
User (Browser)
     ↓
Frontend (React SPA)
     ↓ HTTP
Backend API (Rust, axum/actix)
     ↓
Dream Engine (simulation loop)
     ↓
Agent Runtime  ↔  LLM Provider(s)
     ↓
World Database (SQLite/Postgres)
```

Key principles:

- Agents stateless; world state là single source of truth trong DB.
- Events append-only; mọi mutation đi qua event.
- Simulation chạy theo tick, không realtime từng mili-giây.

---

## 3. Dream Engine & Tick Model

- V1: 1 tick = 5 năm trong world.
- Mỗi tick:
  1. Chọn 2–3 agents hoạt động (trong số các agents sáng tạo).
  2. Lấy world snapshot & recent canonical events.
  3. Gọi Agent Runtime để nhận Event Proposals.
  4. Guardian validate, loại bỏ proposal invalid.
  5. Commit events hợp lệ vào DB.
  6. Historian đánh dấu notable events.

Genisis Mode:
- Chạy batch ticks ban đầu để khởi tạo world.

Evolution Mode:
- Tick đều đặn (loop hoặc job scheduler).

---

## 4. Agent Runtime

- Xây `AgentPrompt` cho từng agent từ world context.
- Gọi `AgentModel` (LLM abstraction) – multi-provider, có **timeout + circuit breaker**.
- Parse output JSON → `EventProposal`.
- **Log call** vào `llm_call_log` (prompt, response, latency, tokens) — cho record/replay và debug.
- Trả về cho Dream Engine/Guardian.

Input rút gọn theo nguyên tắc simulation boundaries trong `ai-dreams-simulation.md`:
- World summary, era summary, region/civ summary.
- 10–30 recent events.
- Entities liên quan.

### 4.1. Mock Provider & Test Harness

`MockAgentModel` trả về response cố định từ fixture files. CI chạy toàn bộ fixtures qua pipeline thật (parse → Guardian → Historian) mà không gọi LLM.

```
fixtures/agents/
  creator/genesis_region.json
  civilization/found_tribe.json
  storyteller/festival.json
```

### 4.2. Error Classification

Mọi error carry metadata: `PipelineStage` (PromptBuild / LlmCall / JsonParse / GuardianValidate / HistorianCanonize / StateCommit), `tick_id`, `agent`, `message`. Metrics group theo stage.

---

## 5. World State Database

V1 dùng **SQLite embedded** (database-per-world: `data/world-{name}.db`) để đơn giản hoá setup; schema tương thích với Postgres để có thể scale sau này.

### 5.1. V1 Core Tables (Sprint 1)

- `worlds`, `regions`, `locations`.
- `civilizations`, `settlements`.
- `events`, `eras`.

### 5.2. Observability Tables (Sprint 2)

- `llm_call_log` — record/replay mọi LLM call.
- `tick_log` — structured metrics per tick.

### 5.3. V2+ Extension Tables (Sprint 7+)

- `creatures`, `resources`, `religions`, `cultures`.
- Tạo khi agent tương ứng được implement; trước đó dùng soft references trong `events.affected_entities` JSON.

Events lưu trữ:
- world_id, year, event_type, agent, description, affected_entities JSON (cũng dùng cho soft references đến entities chưa có table riêng).

---

## 6. Visualization API

- `GET /worlds/current` – world summary.
- `GET /worlds/current/events` – event feed + filters.
- (V2+) `GET /worlds/current/civilizations`, `/timeline`, `/map`, ...

Frontend dùng các endpoint này để render Dream Feed, Timeline, World Overview, etc.

---

## 7. Process Modes & Internal Isolation

Backend hỗ trợ CLI modes: `--mode full` (default), `--mode api-only`, `--mode sim-only`, `--mode single-tick`.

HTTP API và simulation loop chạy trong tokio task groups riêng. Simulation control (pause/resume/tick) qua channel:

```rust
enum SimCommand { Pause, Resume, Tick, Shutdown }
```

LLM calls wrap trong `tokio::time::timeout` (30s) + error counting. Khi provider fail, tick đó bị skip nhưng sim loop và API không crash.

---

## 8. Scalability & Profiles

- V1: single process backend + SQLite (database-per-world), đủ cho 1–vài world, vài user local.
- V2+: profile Postgres/Redis + background worker có thể được thêm mà không đổi core design.
