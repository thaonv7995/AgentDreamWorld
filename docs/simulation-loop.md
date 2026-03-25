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
     - Gọi AgentModel (LLM) để sinh EventProposal.

4. **Validate**  
   - Guardian kiểm tra proposal:
     - narrative physics.
     - world boundaries (size, tick caps).
     - duplication/conflict cơ bản.

5. **Update World**  
   - Commit các events hợp lệ vào DB.
   - Historian đánh dấu notable events.

6. **Notify UI**  
   - Dream Feed & Timeline nhận events mới.

---

## 2. Modes

- **Genesis Mode** – chạy batch ticks đầu để tạo world.
- **Evolution Mode** – tick đều đặn trong thời gian chạy.
- **Fast-forward Mode (V2)** – chạy nhiều ticks liền để nhảy era.
