# AI Dreams World – Visual & AI Image Overview

Tài liệu này phụ trợ cho các file vision/technical/features. Mục tiêu là:

- Làm rõ **triết lý UI/visual** của AI Dreams World.
- Định nghĩa cách **tích hợp AI image** mà không phá core imagination của hệ thống.
- Giữ cho **config người dùng đơn giản nhất có thể**.

---

## 1. Triết lý visual

1. **World sinh từ hư không**  
   - Không có lore, bản đồ hay art nào được hard-code cho từng thế giới.
   - Mọi regions, civilizations, myths, creatures… đều xuất hiện qua chuỗi events do agents sinh ra.

2. **Simulation quyết định thế giới là gì, UI chỉ là cách nhìn**  
   - Dream Engine + world model + events là "sự thật" của thế giới.
   - UI/visual chỉ là lớp biểu diễn state đó (map, timeline, cards, icons...).

3. **Imagination unbounded, visuals bounded**  
   - Agent có thể tưởng tượng rất rộng; không giới hạn theme hay thể loại.
   - Visual system phải đủ linh hoạt để hiển thị đa dạng, nhưng không cố vẽ mọi chi tiết.

4. **AI image là lớp phụ trợ, không phải lõi**  
   - Không cần AI image để world chạy và để user thưởng thức lịch sử/mô phỏng.
   - AI image chỉ dùng để tăng immersion & content, có thể tắt/bật.

---

## 2. Ba lớp visual

### 2.1. Lớp 1 – Structural UI (bắt buộc, không dùng AI image)

Đây là xương sống của Visualization Layer:

- Dream Feed (dòng sự kiện theo thời gian).
- Timeline Explorer.
- World Overview (danh sách regions, civilizations, settlements, religions...).
- Basic Map / Region view (regions, settlements, territories dạng 2D đơn giản).
- Knowledge Graph (graph quan hệ entities).

Assets ở lớp này:

- Layout, typography, màu sắc cơ bản.
- Icons đơn giản cho loại event, stage文明, tech, religion, resource.
- Card frames cho entity cards.

Tất cả đều là **assets tĩnh/procedural** đi kèm repo, không phụ thuộc AI image.

### 2.2. Lớp 2 – Symbolic / Procedural Assets (không cần AI image)

Lớp này tạo bản sắc cho từng world mà vẫn rẻ:

- Civilization sigils / banners (tổ hợp hình-shape + màu + icon đơn giản).
- Religion / cult icons (glyph/rune/pattern procedural).
- Resource / anomaly symbols.

Có thể được tạo bằng:

- Procedural SVG.
- Template compositing (kết hợp các phần tử vector).  

Không yêu cầu AI image – vẫn chỉ là code + static assets.

### 2.3. Lớp 3 – Narrative Art (dùng AI image, optional)

Lớp này tạo **hình ảnh giàu cảm xúc** để quay video, share screenshot, v.v.

- Portrait / hero art cho một số civilizations.
- Concept art cho legendary creatures, gods, artifacts.
- Key art cho major events (great war, cataclysm, prophecy fulfilled...).
- Era splash art (mỗi era một hình mood khác nhau).

Nguyên tắc:

- Chỉ generate art cho **subset nhỏ các entity quan trọng**.
- Generate **once, reuse many times**; không re-generate mỗi lần load UI.
- Có thể hoàn toàn tắt/bật theo setting của người dùng.

---

## 3. Cấu hình AI Image – Multi-provider, đơn giản

### 3.1. Abstraction

Tương tự LLM, tầng image cũng có abstraction riêng:

- `ImageProvider` interface/trait:
  - `generate_image(descriptor) -> Asset`.
- Các implementation:
  - `ImageProvider::Disabled` – không sinh ảnh, dùng placeholder.
  - `ImageProvider::Cloud` – gọi API bên ngoài (Perplexity, OpenAI, v.v.).
  - `ImageProvider::Local` – trỏ tới server nội bộ nếu có.

UI & simulation **không phụ thuộc** vào provider cụ thể – chỉ đọc từ asset registry.

### 3.2. Biến môi trường & setting

Tối thiểu cần:

- `AI_DREAMS_IMAGE_PROVIDER`
  - `none` (default) – không dùng AI image.
  - `perplexity`, `openai`, `local`, ...

- `AI_DREAMS_IMAGE_API_KEY`
  - API key cho provider (nếu dùng cloud).  
  - Không bắt buộc nếu `provider=none` hoặc `local` mà không cần key.

Tùy chọn nâng cao:

- `AI_DREAMS_IMAGE_MAX_ASSETS_PER_WORLD` (ví dụ 50, tránh spam ảnh).
- `AI_DREAMS_IMAGE_STYLE` (một vài preset: `manuscript`, `cosmic_atlas`, `dark_mythic`...).

Mặc định:

- Nếu user không cấu hình gì → `provider=none` → hệ thống không call image API, UI vẫn chạy tốt với structural + symbolic assets.

---

## 4. Pipeline generate image cho một entity

1. **Simulation xác định entity quan trọng**  
   Ví dụ: civilization tồn tại lâu, tham gia nhiều war, là tâm của một era.

2. **Xây visual descriptor**  
   Từ world data + lore:
   - Loại entity (civilization / creature / event / era...).
   - Biome, materials, motifs, palette gợi ý.
   - Mood (ancient, ominous, hopeful...).

3. **Gọi `ImageProvider`**  
   - Chuyển descriptor thành prompt/messages cho provider.
   - Gọi API một lần, nhận về image.

4. **Lưu vào Asset Registry**  
   - Lưu file image (local filesystem / object storage).
   - Lưu metadata: entity_id, style, version, path.

5. **UI hiển thị**  
   - Civilization Viewer / Event Detail / Gallery đọc asset registry để render ảnh.
   - Nếu không có ảnh → fallback sang card symbolic.

---

## 5. Modes sử dụng AI image

Để user dễ hiểu và ít config, có thể có 3 mode đơn giản trong UI Settings:

1. **No Art (default)**  
   - `AI_DREAMS_IMAGE_PROVIDER=none`.
   - Chỉ dùng structural UI + symbolic assets.  
   - Phù hợp cho máy yếu, không muốn gọi API ảnh.

2. **Highlights Only**  
   - Chỉ generate ảnh cho top N entities quan trọng (ví dụ: 3 civ, 5 creatures, 10 events).
   - Tối ưu cho content creator, chi phí vẫn kiểm soát được.

3. **Max Art (advanced)**  
   - Generate nhiều hơn (trong phạm vi `AI_DREAMS_IMAGE_MAX_ASSETS_PER_WORLD`).
   - Chỉ khuyến nghị cho user chấp nhận tốn tài nguyên.

---

## 6. Liên hệ với core imagination

- **Thế giới vẫn sinh từ hư không**: art không phải là source of truth, chỉ phản chiếu world state do agents tạo.
- **Imagination nằm trong event + lore**, không nằm trong assets tĩnh.
- **UI & visuals đọc từ canonical state**:  
  - Map/timeline/feed/graph dựa trên world model + events.  
  - Art chỉ là lớp trang trí, có thể tắt mà world vẫn có hồn.

Nhờ cấu trúc này, AI Dreams World có thể:

- Chạy tối giản chỉ với text + map + icons (không cần AI image).
- Dần dần tăng độ "đẹp" khi user cấu hình thêm image provider.
- Giữ được core vision: **"một thế giới do agent tưởng tượng ra"**, visuals chỉ là cửa sổ nhìn vào giấc mơ đó.
