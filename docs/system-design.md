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
- Gọi `AgentModel` (LLM abstraction) – multi-provider.
- Parse output JSON → `EventProposal`.
- Trả về cho Dream Engine/Guardian.

Input rút gọn theo nguyên tắc simulation boundaries trong `ai-dreams-simulation.md`:
- World summary, era summary, region/civ summary.
- 10–30 recent events.
- Entities liên quan.

---

## 5. World State Database

V1 dùng **SQLite embedded** để đơn giản hoá setup; schema tương thích với Postgres để có thể scale sau này.

Bảng chính:
- `worlds`, `regions`, `locations`.
- `civilizations`, `settlements`.
- `creatures`, `resources`.
- `religions`, `cultures`.
- `events`, `eras`.

Events lưu trữ:
- world_id, year, event_type, agent, description, affected_entities JSON.

---

## 6. Visualization API

- `GET /worlds/current` – world summary.
- `GET /worlds/current/events` – event feed + filters.
- (V2+) `GET /worlds/current/civilizations`, `/timeline`, `/map`, ...

Frontend dùng các endpoint này để render Dream Feed, Timeline, World Overview, etc.

---

## 7. Scalability & Profiles

- V1: single process backend + SQLite, đủ cho 1–vài world, vài user local.
- V2+: profile Postgres/Redis + background worker có thể được thêm mà không đổi core design.
