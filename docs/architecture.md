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
4. Gọi LLM thông qua abstraction `AgentModel`.
5. Parse output thành `EventProposal`.
6. Guardian validate → World Model update.
7. Historian thêm event vào canonical timeline.

---

## 2. Agent Layer

Agent Layer chứa các **AI agents chuyên biệt**:

- Creator Agent – tạo locations, primitive creatures, anomalies.
- Civilization Agent – phát triển tribes → villages → towns → kingdoms → empires.
- Storyteller Agent – sinh narrative events, festivals, discoveries, diplomacy.
- Culture Agent – phong tục, lễ hội, biểu tượng.
- Myth Agent – thần, truyền thuyết, lời tiên tri.
- Ecology Agent – climate, ecosystem, resource distribution.
- Economy Agent – trade routes, currencies, scarcity.
- Chaos Agent – thảm họa, anomaly, mutations.
- Historian Agent – chọn event canonical.
- Guardian Agent – coherence & conflict resolution.

Agents **không giữ state lâu dài**; mọi state của thế giới nằm ở World Model.

---

## 3. World Model

World Model là đại diện có cấu trúc của thế giới, lưu trong DB (V1: SQLite, optional Postgres).

Entity chính:

- World, Region, Location.
- Civilization, Settlement.
- Religion, Culture.
- Creature, Resource.
- Event, Era.

Mọi thay đổi thế giới đi qua **event-sourcing**:

- Bảng `events` append-only.
- World snapshot có thể được dựng lại từ event log.
- Historian đánh dấu subset events là canonical/notable.

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

Optional (V2+):

- Postgres/Redis profile cho scale lớn.
