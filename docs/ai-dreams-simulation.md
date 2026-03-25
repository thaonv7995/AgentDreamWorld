# AI Dreams World – Simulation Boundaries & Layers

Tài liệu này phụ trợ cho **AI Dreams World - Dự án Imagination Engine**, tập trung vào phần **simulation**: giới hạn, tầng diễn tiến và cách giữ cho "giấc mơ" của agent trở thành một thế giới coherent, có thể khám phá được.

---

## 1. Triết lý simulation

- **Agent có thể tưởng tượng rất rộng**, nhưng **thế giới mô phỏng phải có giới hạn rõ** để không biến thành cỗ máy sinh text hỗn loạn.
- Mục tiêu của simulation không phải là chi tiết tối đa, mà là:
  - có lịch sử dễ theo dõi
  - có nền văn minh có động lực
  - có mythology có chiều sâu
  - các sự kiện có quan hệ nhân quả
- Nói gọn: **imagination có thể unbounded, nhưng simulation phải bounded và coherent**.

---

## 2. Sáu lớp giới hạn chính

### 2.1. Giới hạn phạm vi thế giới (World Scope)

V1 **không** nên là "vũ trụ vô hạn". Nên khóa phạm vi thế giới để:
- dễ visualize
- dễ giữ coherence
- dễ debug
- chi phí rẻ hơn nhiều

Đề xuất cấu hình V1:
- 1 world
- 3–4 regions
- 3–6 civilizations active
- tối đa 20 settlements
- 30–100 notable soft-referenced entities / artifacts / anomalies
- khoảng 100–200 major canonical events

Nếu không giới hạn, user sẽ không biết mình đang nhìn cái gì, UI sẽ trở thành mớ hỗn độn khó đọc.

---

### 2.2. Giới hạn theo thời gian mô phỏng (Time Scope)

Không để simulation chạy "real-time vô hạn" ngay từ đầu. Thay vào đó, chia thành 3 mode:

**Genesis mode**
- Dùng để tạo thế giới ban đầu.
- Ví dụ: 50–200 simulation ticks.
- Sinh: geography, climate, primitive creatures, first tribes, first settlements, first notable discoveries.

**Evolution mode**
- Thế giới chạy đều theo nhịp.
- Mặc định V1: 1 tick = 5 năm.
- Mỗi tick sinh 1 major event + tối đa 2 minor events.

**Fast-forward mode**
- Nhảy nhanh qua nhiều năm/era.
- Ví dụ: +50 năm, +100 năm, +1 era.

Cách này giúp user **kiểm soát tiến độ lịch sử**, tránh bị spam event liên tục không đọc nổi.

---

### 2.3. Giới hạn số lượng event mỗi tick

Đây là một trong những giới hạn quan trọng nhất.

**Đề xuất:**
- Mỗi tick chỉ cho phép:
- 1 event lớn
- tối đa 2 event vừa/nhỏ

Ví dụ một tick:
- Creator Agent: mở ra một region bất ổn mới sau biến động địa chất
- Civilization Agent: thành lập một vương quốc mới quanh một settlement chiến lược
- Storyteller Agent: hợp thức hóa lễ đăng quang thành một narrative event đáng nhớ

Không nên để **cả 10 agents** cùng ghi vào world trong một tick, vì sẽ:
- chồng chéo
- mâu thuẫn
- lore bị loạn, khó theo dõi

**Rule gợi ý:**
- Mỗi tick chỉ chọn **2–3 agents** active.
- Historian và Guardian là **hậu xử lý** (validate, ghi timeline), không tính là agent "sáng tạo".

---

### 2.4. Giới hạn độ sâu simulation (Simulation Depth)

AI Dreams **không** nên cố mô phỏng mọi thứ như một game hardcore.

V1 nên chọn mô phỏng ở mức **macro**, cụ thể:
- mô phỏng **nền văn minh**, không phải từng NPC
- mô phỏng **vùng đất**, không phải từng ô tile chi tiết
- mô phỏng **tôn giáo, hệ giá trị**, không phải từng nghi thức nhỏ lẻ
- mô phỏng **chiến tranh, quan hệ quyền lực**, không phải combat từng unit
- mô phỏng **kinh tế cấp cao**, không phải từng route thương nhân

Tóm lại: **history/world simulation**, không phải life sim kiểu The Sims hay Dwarf Fortress full depth.
Nếu đi vào vi mô quá sớm, project sẽ chết vì độ phức tạp và khó visualize.

---

### 2.5. Giới hạn coherence (Narrative Physics)

Simulation phải bị ràng buộc bởi một lớp "luật vật lý narrative" để thế giới **không vô nghĩa**.

Ví dụ giới hạn logic:
- civilization không thể nhảy từ **tribe → empire trong 1 tick** nếu không có event đặc biệt
- religion không thể xuất hiện nếu chưa có **cultural base** hoặc crisis phù hợp
- settlement không thể tồn tại ở vùng không có **resource support** tối thiểu
- creature đã extinct thì không được tham gia war tiếp, **trừ khi có event resurrection**
- tech progression phải theo stage, hoặc có lý do mythic/alien rất mạnh để phá vỡ stage

Nếu không có lớp giới hạn này, world chỉ là chuỗi prompt đẹp nhưng rời rạc, không có cảm giác "thế giới có luật riêng".

---

### 2.6. Giới hạn context cho mỗi agent

LLM không thể đọc toàn bộ lịch sử world mãi mãi. Nếu cố, chi phí cực cao và dễ mất tập trung.

Đề xuất input cho mỗi agent chỉ nên gồm:
- world summary
- current era summary
- affected region / civilization summary
- 10–30 **recent canonical events** liên quan
- danh sách entities liên quan (không phải full DB)

Tức là agent **không đọc toàn bộ database**, mà chỉ đọc:
- snapshot tổng hợp
- context liên quan trực tiếp đến vùng/civilization/myth nó sắp tác động

Đây là điểm cực quan trọng để **scale simulation mà vẫn giữ coherence**.

---

## 3. Các tầng simulation

Để dễ nghĩ và mở rộng, có thể chia simulation thành các tầng:

### Tầng 1 — World Genesis

Sinh ra những thứ nền tảng:
- bản đồ trừu tượng theo `regions`
- climate zones
- primitive creatures
- first tribes
- core anomalies (vùng kỳ dị, phép màu nền)

### Tầng 2 — Civilization Growth

Xây dựng thế giới loài người / civilization:
- settlements (village/town/city)
- trade, alliances
- conflict, wars
- religions, cults *(V2+ hoặc soft reference trong events)*
- customs, festivals, rituals *(V2+ hoặc narrative flavor qua events)*

### Tầng 3 — Era Dynamics

Thay đổi lớn theo thời đại:
- alliances lớn, đế chế nổi lên
- great wars, collapses
- golden ages, renaissances
- major plagues, famines, climate shifts
- canonization của myths *(V2+)* (từ truyền thuyết sang giáo lý chính thức)

### Tầng 4 — Mythic Transformation

Layer mythic/metaphysical của thế giới:
- prophecy fulfilled
- gods emerge / withdraw
- magic rules shift (thay đổi luật chơi của thế giới)
- world rules thay đổi theo meta-events

**V1** nên tập trung làm tốt:
- Tầng 1 + Tầng 2
- Một phần Tầng 3 (những dynamics cơ bản)

Các yếu tố Mythic Transformation có thể xuất hiện ít, như spice, chưa cần quá dày đặc.

---

## 4. Cấu hình simulation hợp lý cho V1

Đây là một cấu hình V1 cân bằng giữa **độ sâu** và **độ phức tạp**:

### 4.1. World size

- 1 world
- 3–4 regions
- 3–6 civilizations active
- 20 settlements (max)
- khoảng 100–200 major events canonical

### 4.2. Tick model

- 1 tick = 5 years
- 2–3 active agents mỗi tick (chọn trong số các agent sáng tạo)
- 1 batch world update được validate & apply mỗi tick

### 4.3. Event caps

Mỗi tick:
- 1 major event
- tối đa 2 minor events

Mỗi era:
- 1 era = 100 years (20 ticks nếu 5 năm/tick)
- 10–20 notable events được đánh dấu trong timeline (không phải mọi event nhỏ lẻ)

### 4.4. Memory & canon

- Raw event log có thể dài hơn, chứa cả event "thường".
- Canonical timeline chỉ giữ lại các event quan trọng.
- Sau mỗi era, world summary được nén lại (compress) để làm context cho các era sau.

---

## 5. Những scope simulation **không nên làm ngay**

Đây là những thứ nghe rất ngầu nhưng cực dễ làm V1 trượt khỏi đường ray:

- mô phỏng từng NPC, từng gia đình
- combat chi tiết từng trận đánh, từng đơn vị quân
- kinh tế quá granular (giá từng món hàng, từng route thương nhân)
- bản đồ 3D procedural full detail như game AAA
- hàng trăm agents cùng hoạt động mỗi tick
- nhiều world song song chạy 24/7 real-time

Những thứ này có thể là mục tiêu dài hạn, nhưng **không phải mục tiêu của V1/V2**.

---

## 6. Cách hiểu đúng về “giới hạn”

Giới hạn simulation **không phải** để làm thế giới nhỏ đi, mà để:

- thế giới **đủ chặt** để người xem hiểu
- lịch sử **đủ rõ** để kể lại
- mythology **đủ sâu** để tạo cảm giác đặc trưng
- event **đủ liên kết** để tạo narrative, chứ không phải spam ý tưởng rời rạc

Mục tiêu không phải **"mọ phỏng mọi thứ"**, mà là:
- **coherent history**
- **meaningful civilizations**
- **rich mythology**
- **explorable world**

Nói gọn: V1 nên là **một world nhỏ nhưng sâu**, với:
- macro simulation thay vì vi mô
- 2–3 agents active mỗi tick
- event cap rõ ràng
- progression rules chặt
- context window rút gọn bằng summaries
- evolution theo era, không chạy realtime vô hạn

---

## 7. Kết nối với vision "imagination engine"

Các giới hạn trên **không mâu thuẫn** với vision "thế giới do agent tự tưởng tượng, không giới hạn sáng tạo":

- Các giới hạn chỉ áp dụng với **phần được chấp nhận vào world canonical**.
- Ở lớp imagination/proposal, agent vẫn có thể đề xuất những ý tưởng điên rồ, bất thường.
- Simulation engine chỉ chọn **một phần trong số đó** để biến thành:
  - sự kiện có hậu quả rõ
  - thay đổi state cụ thể
  - đoạn lịch sử dễ visualize

Nhờ vậy, AI Dreams World vẫn là một **cỗ máy mơ**, nhưng:
- giấc mơ đó có **khung xương lịch sử và địa lý rõ ràng**
- user có thể **theo dõi, hiểu và kể lại** thế giới
- creator có thể **dùng lại** world đó cho MMO / video / blog / game.
