# World State Model – AI Dreams World

World được biểu diễn bằng các entity có cấu trúc, lưu trong DB (V1: SQLite database-per-world, V2+: Postgres).

---

## 1. V1 Core Entities (có table riêng từ Sprint 1)

- **World** – một vũ trụ mô phỏng.
- **Region** – phân chia không gian lớn trong vocabulary canon của V1. Từ `continent` chỉ nên được dùng như nhãn lore/visual, không phải entity riêng.
- **Location** – đảo, rừng, núi, thành phố, dungeon, anomaly, v.v.
- **Civilization** – tập hợp chính trị/xã hội (tribe, kingdom, empire...).
- **Settlement** – điểm dân cư; `village`, `town`, `city` là các subtype/stage, không phải entity gốc khác nhau trong V1 docs.
- **Event** – thay đổi/nút lịch sử.
- **Era** – giai đoạn lịch sử.

## 2. V2+ Extension Entities (soft references trong V1, có table từ Sprint 7+)

Trước khi có table riêng, entities này được lưu dạng **soft references** trong `events.affected_entities` JSON. Khi V2 cần query riêng → migration script extract từ events → backfill tables.

- **Creature** – giống loài/sinh vật.
- **Religion** – hệ thống niềm tin.
- **Culture** – tập tục, lễ hội, biểu tượng.
- **Resource** – tài nguyên quan trọng.

Xem [LIMITATIONS.md](LIMITATIONS.md) §M4 về rationale và migration path.

---

## 3. Relationships (ví dụ)

- Civilization → controls → many Settlements.
- Settlement → located_in → Region.
- Religion → followed_by → many Civilizations. *(V1: qua soft reference)*
- Culture → practiced_by → Civilization. *(V1: qua soft reference)*
- Event → affects → Civilizations / Regions / Creatures.
- Creature → inhabits → Regions. *(V1: qua soft reference)*

Entity không cố định; agent có thể sinh thêm loại phụ, nhưng đây là xương sống để UI & simulation hiểu thế giới.
