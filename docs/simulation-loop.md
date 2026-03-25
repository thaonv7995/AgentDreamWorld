# Simulation Loop – Dream Engine

Dream Engine chạy vòng lặp mô phỏng world theo tick.

---

## 1. Tick Flow (V1)

Pseudo-flow:

1. **Select agents**
   - Chọn 2–3 agents sáng tạo để chạy trong tick này.

2. **Build context**
   - Đọc world summary, era summary.
   - Đọc region/civilization summary liên quan.
   - Lấy 10–30 recent canonical events.

3. **Generate proposals**
   - Với mỗi agent:
     - Build AgentPrompt.
     - Gọi AgentModel (LLM) để sinh EventProposal — **có timeout 30s + circuit breaker**.
     - **Log call** vào `llm_call_log` (prompt, response, latency, tokens).

4. **Validate**
   - Guardian kiểm tra proposal qua **declarative rule engine**:
     - Load rules từ `rules/{event_type}.toml`.
     - Chạy composable validators (entity existence, duplication, progression, world size caps).
     - Log reject reason nếu có.

5. **Update World**
   - Commit các events hợp lệ vào DB.
   - Historian đánh dấu notable events (scoring-based canonicalization).

6. **Log & Notify**
   - **Emit structured tick log** (metrics, reject reasons, cost estimate) vào `tick_log`.
   - Dream Feed & Timeline nhận events mới qua SSE.

---

## 2. Modes

- **Genesis Mode** – chạy batch ticks đầu để tạo world.
- **Evolution Mode** – tick đều đặn trong thời gian chạy.
- **Fast-forward Mode (V2)** – chạy nhiều ticks liền để nhảy era.
- **Single-tick Mode** – chạy đúng 1 tick rồi exit (testing/debugging).
- **Replay Mode** – chạy tick sequence từ recorded LLM responses, không gọi provider thật.

---

## 3. Simulation Control

Simulation loop nhận commands qua channel (không shared mutable state):

```rust
enum SimCommand { Pause, Resume, Tick, Shutdown }
```

- API handler gửi `SimCommand` → sim loop xử lý.
- Pause/resume không cần restart server.
- Manual tick từ `POST /worlds/current/tick` gửi `SimCommand::Tick`.

---

## 4. Process Isolation

HTTP API và simulation loop chạy trong tokio task groups riêng:
- Sim crash → API vẫn sống, user vẫn xem data cũ.
- API crash → sim vẫn chạy, world vẫn tiến hóa.
- LLM timeout → tick bị skip, nhưng không block toàn bộ app.
