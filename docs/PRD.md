# Product Requirements Document – AI Dreams World

## 1. Product Name

**AI Dreams World** – Open-source AI imagination engine & world simulator.

---

## 2. Product Goal

Tạo ra một hệ thống nơi **AI agents tự do tưởng tượng và cùng nhau xây dựng – tiến hóa – thần thoại hóa** một thế giới hư cấu sống động.

Người dùng **không phải là người xây thế giới**, mà là **khán giả/nhà thám hiểm** theo dõi "giấc mơ" đó, có thể thi thoảng ném "God Mode events" để xem thế giới phản ứng.

---

## 3. Target Users

1. **Developers** khám phá multi-agent AI, world simulation.
2. **Writers** tìm cảm hứng worldbuilding, plot, mythology.
3. **Game designers** muốn nền tảng procedural lore/civilization cho game.
4. **Researchers** nghiên cứu emergent behavior, narrative generation.
5. **Hobbyists & content creators** (MMO, video, blog) thích nuôi một vũ trụ ảo để khai thác nội dung dài hạn.

---

## 4. Core Experience

1. Người dùng chạy AI Dreams World (single binary hoặc dev mode).
2. Hệ thống khởi tạo một **world mới từ hư không**:
   - Init agents.
   - Chạy **Genesis Mode** để sinh geography, first tribes, first settlements, 1–2 core anomalies.
3. Sau Genesis, **Evolution Mode** chạy liên tục theo tick (5 năm/tick):
   - Agents sinh event proposals.
   - Guardian validate → world state được cập nhật.
   - Historian ghi canonical timeline.
4. Người dùng:
   - Xem **Dream Feed** như một dòng event cards kể lại thế giới đang đổi thay.
   - Dùng **Timeline** để tua lại lịch sử qua các mốc factual ngắn gọn.
   - Xem **World Overview / civilizations**.
   - Thỉnh thoảng dùng **God Mode** để trigger events và quan sát phản ứng.
5. Khi world đã tích đủ lịch sử, người dùng có thể:
   - Export wiki snapshot.
   - Export annals để làm content.
   - (Phase 2+) Export mythology/myths content khi các agent V2 được bật.

---

## 5. Key Features (high-level)

### 5.1. World Generation & Simulation

- Genesis Mode: tạo world từ hư không (regions, climate rough, primitive creatures, first tribes, anomalies).
- Evolution Mode: thế giới tiến hóa theo tick, agents update world state.
- Simulation boundaries rõ ràng để thế giới vừa **coherent** vừa **explorable**.

### 5.2. Multi-Agent AI

- Catalog tổng thể của dự án gồm 10 agent: Creator, Civilization, Storyteller, Culture, Myth, Ecology, Economy, Chaos, Historian, Guardian.
- V1 runtime chỉ bật 5 thành phần cốt lõi: Creator, Civilization, Storyteller, Historian, Guardian; mỗi tick chỉ chọn 2–3 creative agents active.
- Agent Protocol chuẩn: input là world snapshot + recent canonical events, output là Event Proposal JSON.
- Guardian enforce "narrative physics" để tránh lore hỗn loạn.

### 5.3. Exploration UI

- Dream Feed – stream event cards theo năm, có `title`, summary ngắn và tags để người dùng cảm thấy đang đọc một thế giới sống.
- Timeline Explorer – trục lịch sử factual, sparse hơn Dream Feed, dùng cho zoom theo time range / era và định vị major events.
- World Overview – danh sách regions, civilizations, stats cơ bản.
- (Phase 2+) Civilization Viewer, Region Map, Mythology Browser, Knowledge Graph.

### 5.4. God Mode (Optional)

- Preset world-changing events: meteor strike, new island/region, magical anomaly.
- Thế giới và agents tự xử lý hậu quả.

### 5.5. Content Export

- Wiki snapshot export (Markdown).
- Annals export (biên niên sử notable events).
- Myths & legends export.

---

## 6. Non-goals (V1)

- Không phải game playable: không có avatar, không điều khiển unit.
- Không mô phỏng NPC vi mô, combat chi tiết, kinh tế granular.
- Không yêu cầu Postgres/Redis/K8s để chạy V1 – mặc định dùng SQLite embedded.

---

## 7. Success Criteria (V1)

- Clone repo + config tối thiểu → chạy 1 binary → trong vòng vài phút đã thấy Dream Feed & Timeline có lịch sử đầu tiên.
- Sau vài chục phút chạy, world có:
  - Ít nhất 3–4 civilizations với lịch sử rise/fall sơ bộ.
  - ~100–200 canonical events meaningful.
- Export wiki & annals đọc được, đủ để làm 1–2 video/blog về world đó.
