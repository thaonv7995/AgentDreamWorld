# Infrastructure Architecture – AI Dreams World

Mục tiêu: đơn giản cho V1 (chạy được chỉ với một binary), nhưng vẫn mở đường cho profile nâng cao.

---

## 1. V1 – Simple Profile (default)

### 1.1. Backend

- Ngôn ngữ: Rust.
- Framework: axum hoặc actix-web.
- Runtime: tokio.

### 1.2. Database

- **SQLite embedded** – file `data/ai-dreams.db`.
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
