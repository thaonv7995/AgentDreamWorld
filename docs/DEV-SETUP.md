# AI Dreams World – Dev Setup Guide

Hướng dẫn này mô tả **target setup** cho developer muốn chạy AI Dreams World trên máy của mình khi scaffold code đã được thêm vào repo.

Trạng thái snapshot hiện tại:

- Repo hiện mới chứa docs/specs.
- Các thư mục `crates/server`, `frontend`, `scripts/`, cùng file `.env.example` là **cấu trúc mục tiêu**, chưa có trong snapshot docs-only này.
- Vì vậy, các lệnh bên dưới là contract cho giai đoạn implementation kế tiếp, chưa chạy được ngay trong repo hiện tại.

---

## 1. Yêu cầu môi trường

### 1.1. Bắt buộc

- **Rust** (stable) – cài qua `rustup`.
- **Node.js + npm** – để build & chạy frontend.

### 1.2. Tuỳ chọn (không bắt buộc cho V1)

- **Docker + Docker Compose**  
  - Chỉ cần nếu bạn muốn chạy với Postgres/Redis thay vì SQLite embedded.

---

## 2. Clone & cấu trúc repo (target scaffold)

```bash
git clone https://github.com/yourname/ai-dreams.git
cd ai-dreams
```

Cấu trúc chính dự kiến:

- `crates/server` – backend Rust (Dream Engine + API).
- `frontend` – React + Vite app.
- `docs` – tài liệu (vision, simulation, technical, features, visuals...).

---

## 3. Cấu hình `.env`

Tạo file `.env` từ `.env.example` (sau này sẽ được thêm vào repo):

```bash
cp .env.example .env
```

Trong `.env`, tối thiểu cần điền:

```env
# Provider LLM
AI_DREAMS_LLM_PROVIDER=perplexity   # hoặc openai/local
AI_DREAMS_LLM_API_KEY=your_api_key_here

# (Optional) Image provider – có thể để none
AI_DREAMS_IMAGE_PROVIDER=none
```

Nếu không muốn kết nối LLM (chỉ chạy skeleton), có thể để trống API key và dùng mock provider trong dev.

---

## 4. Chạy ở chế độ dev (backend + frontend riêng)

### 4.1. Cài dependencies frontend

```bash
cd frontend
npm install
cd ..
```

### 4.2. Chạy backend

```bash
cd crates/server
cargo run --bin ai-dreams-server
```

Backend mặc định:

- Nghe ở `http://localhost:3000`.
- Dùng **SQLite embedded** theo kiểu database-per-world (`data/world-main.db` hoặc path cấu hình qua `AI_DREAMS_WORLD_DB`) cho world state.

### 4.3. Chạy frontend

Trong một terminal khác:

```bash
cd frontend
npm run dev
```

Frontend mặc định ở `http://localhost:5173`.

---

## 5. Chạy ở chế độ single-binary (serve static frontend)

Sau khi hệ thống ổn định, có thể dùng script (ví dụ `scripts/dev.sh`) để:

- Build frontend: `npm run build` → `frontend/dist/`.
- Start backend với env `AI_DREAMS_FRONTEND_DIR=frontend/dist` để serve static.

Ví dụ (pseudo):

```bash
./scripts/dev.sh --single
# hoặc
cargo run --release --bin ai-dreams-server
```

Backend sẽ:

- Serve API + static frontend trên cùng một port (vd `http://localhost:3000`).

---

## 6. Profile nâng cao (Postgres/Redis)

Nếu muốn chạy với Postgres/Redis:

1. Start dịch vụ bằng Docker Compose (sau này sẽ có `infra/docker-compose.yml`):

```bash
docker compose up -d postgres redis
```

2. Set `DATABASE_URL` trong `.env` trỏ tới Postgres.

3. Chạy migrations (nếu có).

4. Start backend như bình thường.

V1 không bắt buộc profile này – chỉ dành cho người muốn scale lớn hoặc deploy server.

---

## 7. Quick checklist cho dev mới

- [ ] Cài Rust + Node.
- [ ] Clone repo.
- [ ] Tạo `.env` và điền LLM API key.
- [ ] `npm install` trong `frontend/`.
- [ ] `cargo run` backend + `npm run dev` frontend.
- [ ] Mở `http://localhost:5173` để xem thế giới đang mơ.
