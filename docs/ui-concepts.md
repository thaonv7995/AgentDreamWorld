# UI Concepts – AI Dreams World

UI của AI Dreams World là "cửa sổ" để nhìn vào thế giới mà agents đang mơ. Nó phải **trung tính, data-driven**, không áp đặt lore.

---

## 1. Dream Feed

Real-time (hoặc near real-time) stream của world events.

Ví dụ:

- Year 120 – A tribe settles on Skyroot Island.
- Year 140 – The Storm Bird Festival begins.
- Year 210 – The Skyroot Kingdom forms.

Chức năng:

- Scroll theo thời gian.
- Filter theo event type, agent, civilization, region.

---

## 2. Timeline

Trục thời gian cho world:

- Zoom theo range (10 năm, 100 năm, 1 era).
- Markers cho notable events (được Historian đánh dấu).
- Click marker để xem chi tiết event.

---

## 3. World Overview / Map (V1–V2)

V1:
- Danh sách regions + civilizations + basic stats.

V2:
- Bản đồ 2D stylized:
  - Regions.
  - Settlements (city/town/village).
  - Territory control per civilization.
  - Anomalies (icon trên map).

Map lấy dữ liệu từ World Model, không hard-code layout từng world.

---

## 4. Civilization Viewer (V2)

Cho phép xem chi tiết một civilization:

- Overview: name, stage (tribe/kingdom/empire), rough population.
- History: list notable events liên quan.
- Geography: regions/settlements thuộc civ.
- Society: religions theo, key customs (V2+).

---

## 5. Knowledge Graph (V3)

Graph quan hệ giữa:

- Civilizations ↔ Religions ↔ Myths.
- Wars ↔ Settlements/Regions.
- Creatures ↔ Regions/Myths.

Dùng để khám phá thế giới theo cấu trúc thay vì theo timeline.
