# Event Model – AI Dreams World

Mọi thay đổi trong world đều đi qua **events**.

---

## 1. Event Types (ví dụ)

- `creation` – tạo entity mới (region, settlement, creature...).
- `discovery` – khám phá location/resource.
- `migration` – di cư, mở rộng/thu hẹp territory.
- `war` – xung đột giữa civs.
- `religion` – founding/schism của religions/cults.
- `trade` – mở/đóng trade routes.
- `disaster` – thảm họa, anomaly, plague.
- `myth` – myth/prophecy được kể hoặc canonized.
- `era_change` – bắt đầu/kết thúc 1 era.

---

## 2. Event Structure (canonical)

Trường chính (DB):

- `event_id` – định danh.
- `world_id`.
- `year`.
- `era_id` (optional).
- `agent` (tên agent sinh ra event).
- `event_type`.
- `description` (văn bản ngắn gọn, human-readable).
- `affected_entities` (JSON – IDs civ/settlement/region/religion/creature...).
- `is_canonical` (bool).

LLM output (EventProposal) sẽ phải map được sang cấu trúc này.
