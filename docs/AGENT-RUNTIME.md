# AI Dreams World – Agent Runtime & LLM Integration

Tài liệu này mô tả cách các **agents** trong AI Dreams World tương tác với **LLM** để sinh ra event proposals, và cách hệ thống xử lý chúng thành canonical world state.

---

## 1. Mục tiêu

- Tách rõ **imagination layer** (LLM nghĩ gì cũng được ở dạng proposal) và **simulation layer** (chỉ commit event hợp lệ vào world).
- Hỗ trợ **multi-provider LLM** (Perplexity, OpenAI, local...) qua một abstraction thống nhất.
- Giữ cho **config user đơn giản**: thông thường chỉ cần 1 provider + 1 API key.

---

## 2. Kiến trúc tổng quan

### 2.1. Các tầng chính

1. **Dream Engine**  
   - Chọn agent cho mỗi tick.
   - Chuẩn bị context (world/era/region summary + recent events).

2. **Agent Runtime**  
   - Build `AgentPrompt` từ context + role agent.
   - Gọi `AgentModel` (LLM) để nhận về đáp án.
   - Parse thành `EventProposal` (JSON structured).

3. **Guardian & Rules**  
   - Validate proposal (logic, duplication, progression rules).

4. **World Model & Historian**  
   - Commit event hợp lệ vào DB (canonical state).
   - Ghi vào canonical timeline.

### 2.2. Abstraction `AgentModel`

Interface (pseudo-code):

```rust
struct AgentPrompt { /* world + role + schema info */ }
struct AgentReply { text: String }

#[async_trait]
trait AgentModel {
    async fn complete(&self, prompt: AgentPrompt) -> Result<AgentReply, Error>;
}
```

Implementations:

- `OpenAIModel`
- `PerplexityModel`
- `LocalModel`

Dream Engine & agents **chỉ** gọi qua `AgentModel`, không biết provider cụ thể.

---

## 3. Agent Prompt & Event Proposal

### 3.1. AgentPrompt

Mỗi agent nhận một prompt có cấu trúc gồm:

- **Role**
  - Miêu tả chức năng agent (Creator/Civilization/Storyteller/...).

- **World context** (đã rút gọn theo simulation boundaries của dự án)
  - `world_summary` (tổng quan world hiện tại).
  - `current_era_summary` (bối cảnh thời đại hiện tại).
  - `region/civilization_summary` liên quan (nếu agent tác động vùng/civ cụ thể).
  - 10–30 `recent_events` canonical có liên quan chặt.
  - Danh sách IDs các entity quan trọng (civ, settlement, religion, creature...).

- **Instructions & schema**
  - Yêu cầu agent **chỉ trả lời bằng JSON** theo schema event trong `event-model.md`.

### 3.2. EventProposal

LLM trả về text, nhưng Agent Runtime sẽ parse thành struct `EventProposal` có dạng (ví dụ):

```json
{
  "type": "civilization_foundation",
  "year_offset": 5,
  "agent": "civilization",
  "description": "A new tribe settles near the crystal river.",
  "affected_entities": {
    "region_id": "reg_01",
    "civilization_id": "civ_new",
    "location_id": "loc_river_delta"
  }
}
```

Mọi event proposal phải:

- Có `type` hợp lệ (khớp với `event-model.md`).
- Chỉ tham chiếu entity IDs có thật, hoặc đề xuất entity mới với thông tin đủ.

Nếu parse JSON thất bại, Agent Runtime có thể:

- Thử gọi lại LLM với prompt sửa lỗi.
- Hoặc đánh dấu tick này là lỗi, không commit event gì.

---

## 4. Flow từng tick (chi tiết)

1. Dream Engine chọn agent A cho tick hiện tại.
2. Engine gọi `build_agent_prompt(A, world_state)` → `AgentPrompt`.
3. Agent Runtime gọi `AgentModel.complete(prompt)`.
4. Nhận `AgentReply` (text), parse thành `EventProposal`.
5. Guardian kiểm tra:
   - progression rules (coherence);
   - duplication;
   - constraint về world size, tick caps.
6. Nếu hợp lệ → World Model update + Historian ghi timeline.
7. Nếu không → bỏ qua hoặc sinh một event "null" (no-op / rejected).

---

## 5. Multi-provider configuration

### 5.1. Biến môi trường

Tối thiểu:

- `AI_DREAMS_LLM_PROVIDER`
  - `perplexity` | `openai` | `local` (default tuỳ repo).

- `AI_DREAMS_LLM_API_KEY`
  - API key của provider.

Tùy chọn nâng cao:

- `AI_DREAMS_LLM_MODEL_DEFAULT`
- `AI_DREAMS_LLM_MODEL_MYTH`
- `AI_DREAMS_LLM_MODEL_GUARDIAN`

### 5.2. Mapping provider

- **Perplexity (pplx-api)**  
  - Base URL: `https://api.perplexity.ai`.
  - Endpoint OpenAI-compatible (`/chat/completions`).

- **OpenAI-compatible**  
  - Base URL: `https://api.openai.com/v1`.

- **Local**  
  - Base URL tùy config, ví dụ `http://localhost:8001/chat`.

Mọi provider đều implement `AgentModel`, vì vậy đổi provider chỉ cần đổi env.

---

## 6. Cost & rate control (ở layer Agent Runtime)

Dù triết lý của AI Dreams là "giới hạn duy nhất là phần cứng", Agent Runtime vẫn cần:

- Log mỗi call: agent, world, tick, input_tokens, output_tokens, latency.
- Limit:
  - Số agent active/tick (đã được giới hạn ở simulation layer).
  - Timeout per call.
- Phân chia model:
  - Agents nhẹ (Culture, Economy) → model rẻ/nhỏ.
  - Agents nặng (Storyteller, Myth, Guardian) → model mạnh hơn (optional).

Các logic này nằm trong Agent Runtime, không làm thay đổi core Dream Engine.

---

## 7. Kết nối với các docs khác

- `ai-dreams-simulation.md` – quy định context tối đa mà AgentPrompt được phép đọc.
- `event-model.md` – định nghĩa schema mà EventProposal phải tuân theo.
- `ai-dreams-technical.md` – mô tả tech stack & layout code; Agent Runtime là một module trong backend.
