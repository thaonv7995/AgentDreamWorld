# AI Dreams World – Features Overview

Tài liệu này liệt kê các tính năng chính của hệ thống AI Dreams World, kèm theo **mức độ ưu tiên (V1/V2/Later)** và các **setting tối thiểu** để user có thể chạy với cấu hình ít nhất.

---

## 1. Core Simulation & World

### 1.1. World bootstrap & evolution

- **Auto Genesis World (V1)**  
  Lần chạy đầu, hệ thống tự tạo một world mặc định: 3–4 regions, vài tribes/civilizations, một số anomalies, primitive creatures, first settlements/discoveries. Không cần user chọn gì.

- **Genesis Mode (V1)**  
  Chạy 50–200 ticks khởi tạo: sinh geography, climate, primitive creatures, first tribes, first settlements và first notable discoveries.

- **Evolution Mode (V1)**  
  Simulation tick theo nhịp cố định (1 tick = 5 năm), mỗi tick chỉ sinh 1 major event + tối đa 2 minor events để giữ coherence.

- **Fast-forward Mode (V2)**  
  Cho phép nhảy nhanh +50/+100 năm hoặc +1 era, để “farm” lịch sử nhanh cho mục đích content.

### 1.2. Multi-agent world simulation

- **Dream Engine Loop (V1)**  
  Vòng lặp: chọn agent → đọc world snapshot → agent sinh event proposal → Guardian validate → update world → Historian ghi timeline.

- **Basic Agent Set (V1)**  
  5 thành phần runtime bắt buộc của V1: 3 creative agents (Creator, Civilization, Storyteller) + Historian + Guardian.

- **Full Agent Set (V2)**  
  Catalog đủ 10 agent: thêm Culture, Myth, Ecology, Economy, Chaos.

### 1.3. World model & event sourcing

- **Structured World Model (V1)**  
  World được biểu diễn bằng các entity lõi có cấu trúc: World, Region, Location, Civilization, Settlement, Event, Era. Các entity như Creature/Religion/Culture/Resource ở V1 chỉ đi qua soft references trong `events.affected_entities`, và lên table riêng ở V2+.

- **Event-sourced History (V1)**  
  Mọi thay đổi đi qua event append-only, có thể replay/debug.

- **Era Summaries (V2)**  
  Sau mỗi era, nén world state thành summary để làm context cho các era tiếp theo.

### 1.4. Simulation boundaries

- **World Scope Limits (V1)**  
  1 world, 3–4 regions, 3–6 active civilizations, tối đa 20 settlements, 30–100 notable soft-referenced entities/artifacts/anomalies, khoảng 100–200 major canonical events.

- **Tick & Event Caps (V1)**  
  1 tick = 5 năm; 2–3 agents active/tick; 1 major event + tối đa 2 minor events mỗi tick.

- **Macro-level Simulation Only (V1)**  
  Mô phỏng history/civilization/religion/war/economy cấp cao; không mô phỏng NPC từng cá nhân, combat chi tiết, kinh tế granular.

---

## 2. Visualization & UI

### 2.1. Core views

- **Dream Feed (V1)**  
  Dòng event cards theo năm với `title`, summary ngắn, tags và các entity liên quan; mục tiêu là đọc như đang theo dõi một biên niên sử sống, không phải log thô. Có filter theo loại event, agent, region, civilization.

- **Timeline Explorer (V1)**  
  Trục thời gian factual để xem lịch sử: zoom theo era, nhảy đến time range cụ thể, dùng markers ngắn cho notable events thay vì lặp lại toàn bộ richness của Dream Feed.

- **World Overview (V1)**  
  Danh sách regions + civilizations + basic stats (population rough, development stage, settlement count, canonical event count).

### 2.2. Advanced views

- **Civilization Viewer (V2)**  
  Trang chi tiết cho mỗi civilization: lịch sử, settlements, religion, wars, alliances, tech stage.

- **Region / World Map (V2)**  
  Bản đồ 2D stylized hiển thị regions, settlements, territories, anomalies.

- **Mythology Browser (V2)**  
  Danh sách gods, myths, prophecies, cults với liên kết tới events & civilizations.

- **Knowledge Graph (V3)**  
  Graph tương tác cho quan hệ entities (civilization ↔ religion, war ↔ settlements, myth ↔ region...).

---

## 3. Interaction & God Mode

- **Passive Viewer Mode (V1)**  
  User chỉ cần mở UI, thế giới tự chạy; không cần prompt hay thao tác gì.

- **Simple God Mode (V1)**  
  Một vài nút trigger preset: Meteor Strike, New Island/Region, Magical Anomaly. User chỉ chọn loại & (optionally) region/civilization.

- **Advanced God Mode (V3)**  
  Cho phép config sâu hơn (intensity, scope, type) hoặc custom prompts an toàn.

- **World Pace Control (V2)**  
  Slider chọn tốc độ simulation: Slow / Normal / Fast (ảnh hưởng tick frequency, không cần nhập số cụ thể).

---

## 4. Content & Export

- **Wiki Snapshot Export (V1)**  
  Nút export auto-wiki: sinh một tập file markdown mô tả world summary, civilizations, settlements và major events cho world hiện tại.

- **Annals Export (V1)**  
  Nút xuất “Annals of World X” – biên niên sử các notable events theo trình tự thời gian.

- **Myths & Legends Export (V1/V2)**  
  Export tuyển tập thần thoại & truyền thuyết quan trọng (“Myths of World X”).

- **Story Arc Highlighter (V2)**  
  Gợi ý các arc thú vị: “Rise and Fall of Empire A”, “The Age of Storms”, “Cult of the Ash Moon”.

- **Snapshot Sharing (V2)**  
  Export snapshot 1 era hoặc 1 war/civilization cụ thể (để embed lên blog/video notes).

---

## 5. Multi-world & Community (later)

- **Multi-world Manager (V2)**  
  Màn “Worlds”: danh sách world, nút tạo world mới với vài preset theme (Balanced, High Chaos, Myth-Heavy).

- **World Forking (V3)**  
  Fork world tại một năm X tạo alternate timeline, so sánh outcomes.

- **Community Worlds (Later)**  
  Export/import world (seed + canonical history), gallery các world được share.

- **Collaborative Viewing (Later)**  
  Nhiều user cùng xem 1 world, cùng trigger event trong session chung.

---

## 6. LLM Settings – Multi-provider, ít config

Mục tiêu: **user bình thường chỉ cần nhập 1 API key**, còn provider/model có thể chọn qua config đơn giản.

### 6.1. Abstraction

- **AgentModel abstraction (V1)**  
  Backend không gắn cứng vào 1 provider. Có trait/iface `AgentModel` để gọi model (Perplexity, OpenAI, local…).

- **Per-agent model profiles (V2)**  
  Cho phép cấu hình model khác nhau cho từng nhóm agent (ví dụ Myth/Story dùng model mạnh hơn; Culture/Economy dùng model nhỏ hơn).

### 6.2. Environment & config

Tối thiểu cần các biến:

- `AI_DREAMS_LLM_PROVIDER`  
  Giá trị: `perplexity` | `openai` | `local` (default: `perplexity` hoặc `openai`).

- `AI_DREAMS_LLM_API_KEY`  
  API key của provider đang dùng (1 key duy nhất).

- (Optional nâng cao) `AI_DREAMS_LLM_MODEL_DEFAULT`, `AI_DREAMS_LLM_MODEL_MYTH`, ...

User bình thường:
- Chỉ cần chỉnh 2 dòng trên trong `.env` hoặc màn Settings.

### 6.3. Multi-provider implementation (Later)

- **Perplexity pplx-api**  
  Dùng endpoint OpenAI-compatible, base URL Perplexity; lợi thế inference nhanh, plugin search (tùy tương lai).

- **OpenAI / compatible**  
  Dùng endpoint `/v1/chat/completions` với schema messages.

- **Local LLM**  
  Trỏ tới HTTP server nội bộ (vllm/llama.cpp/khác) – không cần cloud.

---

## 7. Database & Storage – giản lược service tối đa

Mục tiêu: **V1 không bắt buộc Postgres/Redis**, để user không cần nhiều service. Hỗ trợ 2 profile:

### 7.1. Simple profile (V1 default)

- **Embedded database: SQLite**  
  - Dùng SQLite (file `.db` trong thư mục `data/`).
  - Vẫn giữ schema giống Postgres version (tables: worlds, civilizations, events, ...), chỉ khác driver.
  - Phù hợp cho 1 máy, 1 user, 1–vài world.

- **No Redis in V1**  
  - Tick scheduler & cache dùng in-memory trong backend process.
  - Giảm số lượng service phải chạy.

- **Storage**  
  - Local filesystem: `data/`, `exports/`, `assets/`.
  - Export wiki/annals ra markdown/PDF trong thư mục `exports/`.

User bình thường:
- Không cần cài Postgres/Redis.
- Chỉ chạy 1 binary + (tùy chọn) 1 script cài `.env`.

### 7.2. Advanced profile (V2+ option)

Khi cần scale / chạy server cho nhiều user:

- **Postgres mode**  
  - Chạy Postgres ngoài; backend dùng DSN `DATABASE_URL` tương ứng.
  - Có thể chạy nhiều world lớn, nhiều user xem.

- **Redis cache/queue (optional)**  
  - Dùng để giảm tải query & điều phối tick cho nhiều process.

- **Remote object storage (optional)**  
  - S3/MinIO để lưu assets/image/export nếu self-host ở scale lớn.

Tất cả các thứ này là optional – không cần cho V1 desktop/self-host nhỏ.

---

## 8. Dev & Admin Tools

- **Dev Console (V1 basic)**  
  Trang hiển thị số tick, số event, số civilizations, trạng thái world (Running/Paused).

- **Pause/Resume World (V1)**  
  Cho phép tạm dừng/resume simulation cho một world.

- **Event Log Viewer (V2)**  
  Xem event theo agent (debug behavior của Creator/Chaos/Myth...).

- **Config Inspector (V2)**  
  Xem các boundaries hiện tại (world caps, tick caps, model provider, v.v.).

---

## 9. Trải nghiệm user tối thiểu

Với cấu hình mặc định (Simple profile + 1 LLM provider), user chỉ cần:

1. Cài binary (hoặc unzip release).
2. Thêm 1 API key vào `.env` (nếu dùng cloud LLM).
3. Chạy `./ai-dreams`.

Và sẽ có ngay:

- 1 world đang mơ (Genesis + Evolution running).
- Dream Feed + Timeline để xem lịch sử.
- World Overview (regions + civilizations).
- God Mode cơ bản với vài trigger có sẵn.
- Nút export wiki/annals để làm content.

Mọi thứ nâng cao (multi-world, map đẹp, knowledge graph, community) đều để V2/V3/Later – không chặn hành trình build V1.
