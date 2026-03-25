# UI Concepts – AI Dreams World

UI của AI Dreams World là "cửa sổ" để nhìn vào thế giới mà agents đang mơ. Nó phải **trung tính, data-driven**, không áp đặt lore.

---

## 1. Dream Feed

Real-time (hoặc near real-time) stream của world events, nhung duoi dang **narrative cards**.

No khong nen la raw log kieu:

- `Year 120 - A tribe settles on Skyroot Island.`
- `Year 140 - The Storm Bird Festival begins.`

No nen cho cam giac user dang doc lich su cua mot the gioi dang song.

Ví dụ:

- **Year 120**  
  **First Footfall on Skyroot**  
  Ba thuyen Reedborn cap bo phia nam Skyroot sau mot hanh trinh day gio du. Cot khoi dau tien duoc dung len, danh dau khu dinh cu lau dai dau tien tren dao.

- **Year 140**  
  **The Storm Bird Festival Begins**  
  Sau ba mua bao lien tiep, cu dan Skyroot bat dau le hoi treo long chim bac tren mai nha de cau binh an. Nghi le nay nhanh chong tro thanh ban sac chung cua dao.

- **Year 210**  
  **The Skyroot Kingdom Is Proclaimed**  
  Ba thi toc ven dao the chung duoi Cay Goc Troi, ket thuc thoi ky tranh ben cang va lap nen vuong quoc dau tien cua Skyroot.

Chức năng:

- Scroll theo thời gian.
- Filter theo event type, agent, civilization, region.
- Moi card co it nhat: `year`, `title`, `summary`, `type`, `tags`.
- Click card de mo detail va cac entity lien quan.

---

## 2. Timeline

Trục thời gian cho world:

- Zoom theo range (10 năm, 100 năm, 1 era).
- Markers cho notable events (được Historian đánh dấu).
- Click marker để xem chi tiết event.

Timeline co the kho hon Dream Feed. Day la lop dinh vi lich su:

- Year 120 - First Footfall on Skyroot
- Year 140 - Storm Bird Festival begins
- Year 210 - Skyroot Kingdom proclaimed

Nguyen tac:

- `Dream Feed` = ke chuyen.
- `Timeline` = danh dau moc.

Xem them: `DREAM-FEED-COPY-RUBRIC.md`.

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
