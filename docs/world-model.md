# World State Model – AI Dreams World

World được biểu diễn bằng các entity có cấu trúc, lưu trong DB (V1: SQLite, V2+: Postgres).

---

## 1. Core Entities

- **World** – một vũ trụ mô phỏng.
- **Region** – phân chia không gian lớn trong vocabulary canon của V1. Từ `continent` chỉ nên được dùng như nhãn lore/visual, không phải entity riêng.
- **Location** – đảo, rừng, núi, thành phố, dungeon, anomaly, v.v.
- **Civilization** – tập hợp chính trị/xã hội (tribe, kingdom, empire...).
- **Settlement** – điểm dân cư; `village`, `town`, `city` là các subtype/stage, không phải entity gốc khác nhau trong V1 docs.
- **Creature** – giống loài/sinh vật.
- **Religion** – hệ thống niềm tin.
- **Culture** – tập tục, lễ hội, biểu tượng.
- **Resource** – tài nguyên quan trọng.
- **Event** – thay đổi/nút lịch sử.
- **Era** – giai đoạn lịch sử.

---

## 2. Relationships (ví dụ)

- Civilization → controls → many Settlements.
- Settlement → located_in → Region.
- Religion → followed_by → many Civilizations.
- Culture → practiced_by → Civilization.
- Event → affects → Civilizations / Regions / Creatures.
- Creature → inhabits → Regions.

Entity không cố định; agent có thể sinh thêm loại phụ, nhưng đây là xương sống để UI & simulation hiểu thế giới.
