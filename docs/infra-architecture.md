# Infrastructure Architecture – AI Dreams World

Mục tiêu: đơn giản cho V1 (chạy được chỉ với một binary), nhưng vẫn mở đường cho profile nâng cao.

---

## 1. V1 – Simple Profile (default)

### 1.1. Backend

- Ngôn ngữ: Rust.
- Framework: axum hoặc actix-web.
- Runtime: tokio.

### 1.2. Database

- **SQLite embedded**, database-per-world: `data/world-{name}.db`.
- Copy file = clone world, đổi env = switch world.
- Không yêu cầu Postgres cho V1.

### 1.3. Cache & Queue

- In-memory trong process backend.
- Không yêu cầu Redis cho V1.

### 1.4. Frontend

- React + Vite SPA.
- Dev: chạy `npm run dev`.
- Prod: build ra `frontend/dist`, backend serve static.

### 1.5. Deployment

- Single binary `ai-dreams-server` (serve API + static frontend).
- Optional: binary + SQLite file chạy trên bất kỳ máy nào có Rust runtime.

### 1.6. Process Modes

```bash
ai-dreams-server                    # Full mode — API + simulation
ai-dreams-server --mode api-only    # Chỉ HTTP (frontend dev)
ai-dreams-server --mode sim-only    # Chỉ simulation (debug tick)
ai-dreams-server --mode single-tick # Chạy 1 tick rồi exit (testing)
```

HTTP API và simulation loop isolated trong tokio task groups riêng, giao tiếp qua channel.

### 1.7. Observability (từ Sprint 2)

- Structured tick log (JSONL hoặc SQLite table `tick_log`).
- `llm_call_log` table cho record/replay.
- CLI report: `ai-dreams-server report --last N`.
- Cost alert khi cost/tick vượt threshold.

---

## 2. V2+ – Advanced Profile (optional)

### 2.1. Backend & DB

- Database: Postgres.
- Cache & queue: Redis.
- Migration từ SQLite schema sang Postgres.

### 2.2. Deployment

- Docker Compose: backend + Postgres + Redis.
- Sau này có thể: Kubernetes, scaling multi-world.

---

## 3. LLM & Image Providers

- LLM: cấu hình qua env (`AI_DREAMS_LLM_PROVIDER`, `AI_DREAMS_LLM_API_KEY`).
- Image: cấu hình qua env (`AI_DREAMS_IMAGE_PROVIDER`, `AI_DREAMS_IMAGE_API_KEY`).

Backend chỉ gọi provider qua abstraction, không phụ thuộc vendor cụ thể.
