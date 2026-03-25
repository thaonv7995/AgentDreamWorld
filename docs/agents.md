# Agent System – AI Dreams World

AI Dreams World sử dụng một tập các **agents chuyên biệt** để cùng nhau tạo và tiến hóa thế giới.

---

## 0. Source of Truth cho V1 / V2

Tài liệu này là **source of truth** cho phạm vi agent của dự án khi có khác biệt giữa vision docs, roadmap, và technical docs.

### Quy ước chuẩn

- **V1 runtime** luôn có **5 thành phần cốt lõi**:
  - 3 **creative agents**: `Creator`, `Civilization`, `Storyteller`
  - 2 **runtime guardrails**: `Historian`, `Guardian`
- Mỗi tick chỉ chọn **2–3 creative agents** active.
- `Historian` và `Guardian` luôn chạy ở bước hậu xử lý, **không tính** vào quota 2–3 creative agents/tick.
- **V2** mở rộng catalog agent bằng `Culture`, `Myth`, `Ecology`, `Economy`, `Chaos`.

### Agent Matrix

| Agent | Phase | Role type | Có thể là creative agent active/tick | Luôn chạy trong V1 runtime | Ghi chú |
| --- | --- | --- | --- | --- | --- |
| Creator | V1 | Creative | Có | Có | Sinh geography, anomalies, primitive entities |
| Civilization | V1 | Creative | Có | Có | Sinh và tiến hóa civilizations, settlements |
| Storyteller | V1 | Creative | Có | Có | Tạo narrative events |
| Historian | V1 | Post-processing | Không | Có | Chọn canonical events, viết era summary |
| Guardian | V1 | Validation | Không | Có | Validate coherence, progression, entity refs |
| Culture | V2 | Creative | Có | Không | Customs, rituals, symbols |
| Myth | V2 | Creative | Có | Không | Gods, legends, prophecies |
| Ecology | V2 | Creative | Có | Không | Climate, ecosystems, habitat shifts |
| Economy | V2 | Creative | Có | Không | Trade, resources, scarcity |
| Chaos | V2 | Creative | Có | Không | Disasters, mutations, destabilizing events |

---

## 1. Creator Agent

Nhiệm vụ:

- Tạo entities mới:
  - Regions/locations (đảo, núi, sa mạc, archipelago...).
  - Primitive creatures.
  - Core anomalies (vùng kỳ dị, ma thuật nền).

---

## 2. Civilization Agent

Nhiệm vụ:

- Sinh & phát triển nền văn minh:
  - tribes → villages → towns → kingdoms → empires.
  - Mở rộng/thu hẹp territory.
  - Thành lập/dời hoặc nâng cấp settlements.

---

## 3. Storyteller Agent

Nhiệm vụ:

- Sinh **narrative events**:
  - discoveries, festivals, diplomacy, intrigues.
  - big social turning points.

---

## 4. Culture Agent (V2)

Nhiệm vụ:

- Lễ hội, rituals, customs, symbols.
- Tạo cultural identity cho civilizations.

---

## 5. Myth Agent (V2)

Nhiệm vụ:

- Gods, myths, legends, prophecies.
- Chuyển events & anomalies thành mythology.

---

## 6. Ecology Agent (V2)

Nhiệm vụ:

- Climate, ecosystems.
- Habitat của creatures.
- Environmental shifts.

---

## 7. Economy Agent (V2)

Nhiệm vụ:

- Trade routes.
- Rough economic relations between civs.
- Resource scarcity/abundance events.

---

## 8. Chaos Agent (V2)

Nhiệm vụ:

- Thảm họa, mutations, anomalies bất ngờ.
- Dark events phá vỡ trạng thái cân bằng.

---

## 9. Historian Agent

Nhiệm vụ:

- Chọn events nào là **canonical/notable**.
- Viết summary ngắn cho mỗi era.

---

## 10. Guardian Agent

Nhiệm vụ:

- Coherence & consistency:
  - Reject impossible events (phá progression quá lố, dùng ID không tồn tại...).
  - Resolve lore conflicts.
  - Enforce world rules (simulation boundaries & narrative physics).

---

## 11. Agent Properties

- Stateless – không giữ long-term state ngoài DB.
- Input: AgentPrompt (world/era/region summary + recent events + instructions + schema).
- Output: EventProposal JSON.
