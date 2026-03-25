# AI Dreams World

AI Dreams World là một **AI imagination engine & world simulation** mã nguồn mở – nơi các AI agents cùng nhau mơ ra một vũ trụ hư cấu, còn bạn ngồi xem nó lớn lên.

Thay vì trả lời prompt trực tiếp, các agent sẽ:

- Tạo môi trường & bản đồ.
- Xây dựng nền văn minh.
- Sinh thần thoại & truyền thuyết.
- Mô phỏng lịch sử.
- Gây ra hỗn loạn & biến đổi.

Bạn khám phá thế giới qua:

- Dream Feed (dòng sự kiện theo thời gian).
- Timeline (biên niên sử).
- World Overview (regions, civilizations, settlements...).
- (Sau này) Map, Civilization Viewer, Mythology Browser, Knowledge Graph.

---

## Vision

Tạo ra một **"máy mơ"** nơi:

- Mỗi world sinh ra từ hư không.
- Agents liên tục tưởng tượng & sửa đổi world state.
- Lịch sử, thần thoại, nền văn minh emergent theo thời gian.
- Người dùng có thể ngồi quan sát, đôi lúc kích hoạt God Mode, và thu hoạch nội dung (MMO/video/blog).

Xem thêm: `ai-dreams-vision.md`.

---

## Current Status

- Snapshot repo hiện tại là **docs-only**: mới chứa product/architecture/spec docs.
- Chưa có scaffold backend/frontend trong snapshot này, nên các lệnh chạy app trong tài liệu setup hiện mới là **target-state contract** cho giai đoạn code scaffold tiếp theo.
- Khi bắt đầu implementation, ưu tiên đọc:
  - `MVP-SPEC.md` cho phạm vi V1.
  - `agents.md` cho agent matrix và runtime roles.
  - `world-model.md` + `database-schema.md` cho vocabulary canon (`Region`, `Settlement`).

---

## Project Docs

- Product: `PRD.md`.
- Vision: `ai-dreams-vision.md`.
- Agent Matrix & Runtime Roles: `agents.md`.
- Agent Instructions: `AGENT-INSTRUCTIONS.md`.
- Agent Specs: `agent-specs/README.md`.
- Architecture: `architecture.md`.
- System Design: `system-design.md`.
- Simulation: `ai-dreams-simulation.md`.
- Technical Overview: `ai-dreams-technical.md`.
- Features: `FEATURES.md`.
- Visuals & AI Image: `ai-dreams-visuals.md`.
- MVP spec: `MVP-SPEC.md`.
- API Contract: `API-CONTRACT.md`.
- API Codes: `API-CODES.md`.
- Implementation Plan: `IMPLEMENTATION-PLAN.md`.
- Project Master Plan: `PROJECT-MASTER-PLAN.md`.
- Sprint Library: `sprints/README.md`.
- Sprint Master Backlog: `sprints/MASTER-BACKLOG.md`.
- Agent Runtime & LLM: `AGENT-RUNTIME.md`.
- Guardian Rulebook: `GUARDIAN-RULEBOOK.md`.
- Test & Eval Strategy: `TEST-AND-EVAL-STRATEGY.md`.
- Dev setup: `DEV-SETUP.md`.

---

## Tech Stack (high-level)

- Backend: Rust (axum/actix, tokio).
- Storage: SQLite (V1), optional Postgres/Redis.
- LLM: multi-provider (Perplexity/OpenAI/local) qua abstraction.
- Frontend: React + Vite.

Chi tiết hơn: `ai-dreams-technical.md`.

---

## Getting Started (khi scaffold code đã có)

Xem `DEV-SETUP.md` để biết cách cài & chạy project local khi backend/frontend scaffold đã được thêm vào repo.

Luồng chạy dự kiến:

```bash
git clone ...
cd ai-dreams
cp .env.example .env   # (sau này)
# Điền LLM API key vào .env

cd frontend
npm install
npm run dev

# Terminal khác
cd crates/server
cargo run --bin ai-dreams-server
```

Mở `http://localhost:5173` để xem thế giới đang mơ.
