# AI Dreams World – Technical Overview

Tài liệu này phụ trợ cho các file vision/architecture/simulation, tập trung vào phần **technical** ở level kiến trúc & stack (chưa đi vào code chi tiết).

Mục tiêu:
- Dễ hiểu cho contributor mới
- Dễ build thành **một repo, một binary**
- Phù hợp với kiến trúc Dream Engine + Agent Layer + World Model + Visualization Layer

---

## 1. Mục tiêu kỹ thuật

1. **Single repo, single binary**
   - Clone repo → chạy 1–2 lệnh → có AI Dreams chạy cục bộ.
   - Dev: backend + frontend chạy riêng để HMR nhanh.
   - Prod/dev-parity: build frontend, backend serve static → 1 binary chính.

2. **Engine-first, UI-second**
   - Core là Dream Engine + world simulation.
   - UI chỉ là lớp khám phá (map, feed, timeline, graph) đọc từ canonical state.

3. **Open-source-friendly**
   - Stack phổ biến, dễ cài (Rust, Node, SQLite; optional Postgres/Redis cho profile nâng cao).
   - Docker Compose chỉ cần cho profile nâng cao.
   - Scripts dev rõ ràng (giống `dev.sh` bạn dùng ở ACPMS).

---

## 2. Tech stack tổng quan

### 2.1 Backend – Dream Engine & API

- Ngôn ngữ: **Rust**
- Framework API: `axum` hoặc `actix-web`
- Runtime async: `tokio`

Vai trò:
- Expose HTTP API cho frontend (REST/WebSocket nếu cần live feed).
- Chạy **simulation loop** (Dream Engine) theo tick.
- Orchestrate calls tới các agent (LLM) và Guardian.
- Đọc/ghi world state và events trong storage layer của world.

### 2.2 Agent runtime / LLM integration

- HTTP client: `reqwest`
- Interface trừu tượng: trait `AgentModel` (OpenAI/Anthropic/local… đều implement được).
- Tổ chức agent theo domain: `Creator`, `Civilization`, `Storyteller`, `Culture`, `Myth`, `Economy`, `Ecology`, `Chaos`, `Historian`, `Guardian`.
- Kiến trúc **proposal → validation → canonical event**:
  - Agent sinh proposal (imagination layer).
  - Guardian + rule engine validate.
  - Dream Engine commit vào canonical world state (simulation layer).

### 2.3 Database & storage

- **SQLite embedded (V1 default)** – world model + event log.
  - File mặc định: `data/ai-dreams.db`.
  - Bảng chính: `worlds`, `regions`, `locations`, `civilizations`, `settlements`, `creatures`, `events`, `religions`, `cultures`, `resources`, `eras`, ...
  - Event-sourcing cho world changes (append-only `events`).
- **Postgres (V2+/optional)** – cùng schema, dùng khi cần scale lớn hơn hoặc multi-user.
- **Redis (V2+/optional)** – cache + queue nhẹ:
  - Cache world summaries / era summaries.
  - Tick scheduling, background jobs đơn giản.

### 2.4 Frontend – Visualization layer

- **React** (TypeScript nếu muốn)
- Bundler: **Vite** (dev HMR nhanh, build dist cho single-binary mode)
- Visualization libs:
  - Map / regions: SVG/Canvas + D3/PixiJS.
  - Knowledge graph: Cytoscape.js hoặc d3-force.

Components chính:
- Dream Feed (event stream theo thời gian).
- Timeline Explorer.
- World Overview / Map (V1 có thể là region map abstractions).
- Civilization Viewer.
- Mythology / Knowledge Graph.

---

## 3. Layout repo đề xuất

Cấu trúc tối thiểu cho một repo duy nhất:

```text
ai-dreams/
  crates/
    server/           # Backend Rust: Dream Engine + API
      src/
        main.rs
        lib.rs
        api/          # HTTP handlers
        core/         # domain: world, events, simulation rules
        agents/       # agent protocol + adapters LLM
        infra/        # DB, config, logging, optional integrations
  frontend/           # React + Vite app
    src/
    index.html
  docs/
    ai-dreams-vision.md
    architecture.md
    system-design.md
    ai-dreams-simulation.md
    PRD.md
  infra/
    docker-compose.yml # optional advanced profile
  scripts/
    dev.sh
  README.md
  Cargo.toml
  package.json
```

- `crates/server` chứa toàn bộ logic backend.
- `frontend` là SPA, build ra `dist/` để backend serve.
- `docs` tái sử dụng các file đang có + file mới (simulation, vision, tech).
- `infra` có thể chứa compose để dựng Postgres + Redis cho profile nâng cao.

---

## 4. Dev workflow & single-binary mode

### 4.1 Mục tiêu

- Dev nhanh: backend + frontend chạy riêng (HMR, hot reload).
- Test prod-parity: single binary serve static frontend.
- Script dev 1 lệnh, giống ACPMS.

### 4.2 Script `scripts/dev.sh` (ý tưởng)

Các mode chính:

1. **Mặc định** – dev mode:
   - Start backend: `cargo run --bin ai-dreams-server`.
   - Start frontend: `npm run dev` (Vite) ở `http://localhost:5173`.
   - Dùng **SQLite embedded** mặc định, không cần thêm service.

2. **`--single` / `--binary`** – single binary dev mode:
   - Build frontend: `npm run build` → `frontend/dist/`.
   - Start backend: `cargo run --bin ai-dreams-server` với env `AI_DREAMS_FRONTEND_DIR=frontend/dist`.
   - Backend serve static từ thư mục này tại `http://localhost:3000`.

3. **`--parity`** – production-parity mode:
   - Build backend release: `cargo build --release --bin ai-dreams-server`.
   - Build frontend (nếu chưa có).
   - Run binary release với env gần giống production (APP_ENV=production,...).

Nếu muốn test profile nâng cao:
- Start Postgres + Redis từ `infra/docker-compose.yml`.
- Set `DATABASE_URL` và các biến cache/queue tương ứng.

Ý tưởng tương tự script ACPMS của bạn: **một entrypoint để chạy hết cả stack dev**.

---

## 5. Mối quan hệ giữa technical & simulation docs

- `ai-dreams-vision.md` + `PRD.md` mô tả **tại sao** và **trải nghiệm**.
- `ai-dreams-simulation.md` mô tả **thế giới vận hành thế nào, giới hạn ra sao**.
- File này (Technical Overview) mô tả **bằng gì** và **tổ chức code + infra thế nào** để thực hiện được các docs kia.

Ánh xạ:
- Dream Engine & Agent Layer → `crates/server/core` + `crates/server/agents` như mô tả trong `architecture.md`.
- World Model (schema tương thích Postgres, mặc định chạy trên SQLite ở V1) → `crates/server/infra/db` + migrations.
- Simulation Loop → task/tick runner trong backend Rust như mô tả trong `simulation-loop.md`.
- Visualization Layer → `frontend/` React app như mô tả trong `ui-concepts.md`.

---

## 6. Hướng triển khai từng phase (technical)

### Phase 1 – Core Engine + Basic UI

Backend:
- Implement world schema + migrations.
- Implement minimal event model + append-only log.
- Implement Dream Engine loop cơ bản (select agent → generate event → Guardian → commit → Historian).
- Implement 5 agents đầu tiên của V1: Creator, Civilization, Storyteller, Historian, Guardian.

Frontend:
- Dream Feed UI (list event, filter theo năm/loại/agent).
- Simple Timeline (thanh thời gian, scroll / jump theo range).
- Simple World Overview (list regions + civilizations, chưa cần map phức tạp).

Infra:
- Mặc định chạy SQLite embedded, không cần service ngoài.
- Script `dev.sh` với 2 mode chính: dev + single.
- Docker Compose cho Postgres/Redis là optional nếu cần test profile nâng cao.

### Phase 2 – Expanded Simulation & Mythology

Backend:
- Thêm agents: Culture, Myth, Ecology, Economy, Chaos.
- Áp dụng **simulation boundaries**: caps world size, events/tick, macro depth.
- Bắt đầu era summaries (nén world state theo từng era).

Frontend:
- Civilization Viewer (chi tiết 1 civilization).
- Basic map view (regions + ownership).
- Mythology list (góc nhìn theo gods/myths).

### Phase 3 – Visualization & Export

Backend:
- Projections cho map, graph, highlights.
- Export endpoints cho wiki / annals / myths.

Frontend:
- Knowledge Graph view.
- World Map nâng cao.
- Tools export (copy lore, share events, v.v.).

---

## 7. Nguyên tắc thiết kế kỹ thuật

1. **Domain-first**
   - Simulation logic (world, events, rules) phải nằm trong core module độc lập with web.
2. **Event-sourced**
   - Mọi thay đổi world phải đi qua event, dễ debug & replay.
3. **Imagination vs Canonical**
   - Agent có thể generate bất kỳ ý tưởng nào, nhưng chỉ canonical events mới vào world.
4. **Configurable boundaries**
   - Mọi giới hạn (world size, events/tick, etc.) là config, không hard-code.
5. **Observable**
   - Log events, metrics tick time, số token/agent (sau này), để tune chi phí.
