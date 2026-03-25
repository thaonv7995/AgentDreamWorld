# AI Dreams World – MVP Specification (V1)

Mục tiêu của tài liệu này là **khóa scope cho V1 (MVP)** của AI Dreams World – một prototype có thể chạy được, đủ để:

- Khởi tạo một world từ "hư không".
- Cho agents tự sinh lịch sử & thần thoại theo thời gian.
- Cho user quan sát world qua Dream Feed, Timeline và World Overview.

---

## 1. Mục tiêu V1

### 1.1. Mục tiêu sản phẩm

- Cho phép user:
  - Chạy một world duy nhất trên máy của mình.
  - Xem thế giới đó được khởi tạo (Genesis) và tiến hóa (Evolution) theo thời gian.
  - Quan sát các nền văn minh hình thành, phát triển, sụp đổ.
  - Xuất ra wiki/annals cơ bản để làm content.

### 1.2. Mục tiêu kỹ thuật

- Một binary backend (Rust) + một frontend (React) trong cùng repo.
- Sử dụng **SQLite embedded** làm storage mặc định (không cần Postgres/Redis cho V1).
- Kết nối 1 provider LLM (Perplexity/OpenAI/local) qua abstraction `AgentModel`.

---

## 2. Phạm vi simulation V1

### 2.1. World scope

- 1 world duy nhất.
- 3–4 regions.
- Tối đa 6 civilizations active.
- Tối đa 20 settlements (town/city/village).
- Khoảng 100–200 major events canonical.

### 2.2. Tầng simulation

V1 cover tốt:

- **Tầng 1 – World Genesis**
  - Sinh regions, climate rough, primitive creatures (qua soft references), first tribes, 1–2 core anomalies.

- **Tầng 2 – Civilization Growth**
  - Sinh settlements, civs, trade thô, conflict cơ bản.

- Tầng 3 (Era Dynamics) mới ở mức **rất sơ khai** – chỉ một số war/collapse lớn.

### 2.3. Tick model & caps

- 1 tick = 5 năm (game time).
- Mỗi tick:
  - Chọn 2–3 agents sáng tạo.
  - Cho phép 1 major event + tối đa 2 minor events.
- Raw events có thể nhiều, nhưng canonical timeline V1 chỉ giữ khoảng 100–200 major events.

---

## 3. Agents trong V1

### 3.1. Danh sách thành phần agent/runtime bắt buộc

1. **Creator Agent**  
   - Sinh locations, primitive creatures, basic anomalies.

2. **Civilization Agent**  
   - Thành lập tribes → villages → towns, mở rộng/thu hẹp civs theo thời gian.

3. **Storyteller Agent**  
   - Tạo narrative events (festivals, discoveries, diplomatic events...).

4. **Historian Agent**  
   - Chọn sự kiện quan trọng để ghi vào canonical timeline.

5. **Guardian Agent**  
   - Validate event proposal (logic, duplicate, basic progression rules).

Rule runtime V1:

- Mỗi tick chỉ chọn **2–3 creative agents** active từ `Creator`, `Civilization`, `Storyteller`.
- `Historian` và `Guardian` luôn chạy sau bước proposal, không tính vào quota 2–3 agents active/tick.
- Guardian dùng **declarative rule engine** — rules định nghĩa trong `rules/{event_type}.toml`, composable validators.
- Historian dùng **scoring-based canonicalization** — không hardcode, có thể tune qua config.
- Các agents khác (`Culture`, `Myth`, `Ecology`, `Economy`, `Chaos`) là optional/V2 – có thể mock hoặc disable từng phần.

### 3.2. Agent Protocol V1

- Input chung cho mọi agent:
  - `world_summary`
  - `current_era_summary`
  - `region/civilization_summary` liên quan
  - 10–20 `recent_events` liên quan
  - danh sách entity IDs có liên quan trực tiếp.

- Output: một **Event Proposal JSON** tuân theo `event-model.md`.

---

## 4. API & backend V1

### 4.1. API chính

Không cần full REST spec, chỉ cần các nhóm endpoint:

- **World info**
  - `GET /worlds/current` – trả về summary world hiện tại.

- **Events & timeline**
  - `GET /worlds/current/events` – trả về list/paged events (canonical trước, raw optional).
  - Query params: `from_year`, `to_year`, `type`, `agent`, `civilization_id`.

- **Tick / simulation control**
  - V1 có thể tick background, nhưng thêm endpoint:  
    - `POST /worlds/current/tick` – trigger 1 tick thủ công (cho dev/debug).

- **Export**
  - `POST /worlds/current/export/wiki`
  - `POST /worlds/current/export/annals`

### 4.2. Backend runtime

- Service duy nhất `ai-dreams-server`, hỗ trợ **process modes**:
  - `--mode full` (default): HTTP API + simulation loop.
  - `--mode api-only`: chỉ HTTP (cho frontend dev).
  - `--mode sim-only`: chỉ simulation (cho debug tick).
  - `--mode single-tick`: chạy đúng 1 tick rồi exit (cho testing).
- HTTP API và simulation loop chạy trong tokio task groups riêng, giao tiếp qua channel.
- LLM client (AgentModel) có timeout 30s + circuit breaker.
- SQLite access: database-per-world (`data/world-{name}.db`).

---

## 5. Frontend V1

### 5.1. Views bắt buộc

1. **Dream Feed**  
   - List event theo thời gian (Year, title, short description, type, tags).

2. **Timeline View**  
   - Trục thời gian, hiển thị markers cho major events, cho zoom theo range.

3. **World Overview**  
   - Danh sách regions, civilizations, số settlements, vài chỉ số rough.

### 5.2. Interaction tối thiểu

- Chọn một civilization để filter events liên quan.
- Tùy chọn: một nút **God Mode đơn giản** (1–2 preset event) – nếu có thời gian.

Không yêu cầu map 2D đầy đủ, knowledge graph, hay UI art phức tạp trong V1.

---

## 6. LLM & storage profile cho V1

- **LLM**
  - 1 provider, 1 API key, 1 model default là đủ.
  - Cấu hình qua `.env`: `AI_DREAMS_LLM_PROVIDER`, `AI_DREAMS_LLM_API_KEY`.

- **Storage**
  - SQLite embedded, database-per-world (`data/world-{name}.db`).
  - Export files (wiki/annals) trong `exports/`.

- **Observability (từ Sprint 2)**
  - Structured tick log: tick_id, agents, proposals accepted/rejected, reject reasons, tokens, latency, cost.
  - `llm_call_log` table: record/replay mọi LLM call.
  - CLI report: `ai-dreams-server report --last N`.
  - Không cần Grafana/Prometheus cho V1.

- **Test Harness**
  - `MockAgentModel` + fixture files cho deterministic testing.
  - Snapshot testing: golden world state sau N mock ticks.
  - Contract tests cho API response shapes.

Postgres/Redis/remote storage là lựa chọn V2+, không bắt buộc cho MVP.

---

## 7. Definition of Done cho V1

V1 được coi là xong khi:

1. Chạy được binary `ai-dreams-server` + frontend → tự tạo world mới từ hư không.
2. Sau 5–10 phút, Dream Feed & Timeline hiển thị được lịch sử cơ bản của world.
3. Có ít nhất 3–4 civilizations hình thành & biến đổi theo thời gian.
4. Export wiki + annals chạy ổn và readable.
5. Toàn bộ chạy được với cấu hình tối thiểu:  
   - 1 API key cho LLM.  
   - Không cần Postgres/Redis.
