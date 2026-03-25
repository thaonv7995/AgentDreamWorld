# Sprint 07 – Culture, Myth, Era Summaries

## Sprint Metadata

| Field | Value |
| --- | --- |
| Phase | Phase 4 – Expanded Simulation |
| Milestone Gate | Gate E – Expanded Simulation Ready |
| Suggested Duration | 2 tuần |
| Primary Validation Signal | World có layer culture/myth/era summary đủ rõ để dùng cho lore và agent context |
| Source Backlog IDs | `ADW-S07-BA-01`, `ADW-S07-BE-01`, `ADW-S07-FE-01`, `ADW-S07-DO-01` |

## Sprint Goal

Làm cho world có chiều sâu văn hóa và thần thoại rõ ràng hơn sau MVP.

## Business Objective

Mở rộng simulation từ “history vận hành được” sang “lore có bản sắc”, để sản phẩm bắt đầu có chiều sâu content đáng nhớ.

## Business Value

- Tăng richness của world narrative.
- Giảm phụ thuộc vào event log quá dài bằng era summaries.
- Tạo nền cho Mythology Browser và graph ở các sprint sau.

## In Scope

- Culture Agent.
- Myth Agent.
- Era summaries.
- Context compression bước đầu.
- Event tagging/myth-culture projection cơ bản.

## Out of Scope

- Ecology/Economy/Chaos.
- Region map.
- Civilization Viewer đầy đủ.
- Knowledge Graph.

## Primary User Stories

- Với vai trò **writer/content creator**, tôi muốn world có customs và myths rõ ràng để dùng làm chất liệu kể chuyện.
- Với vai trò **runtime owner**, tôi muốn era summaries để giảm chi phí context và giữ coherence.
- Với vai trò **product lead**, tôi muốn chứng minh post-MVP world không chỉ nhiều event mà còn có bản sắc.

## Acceptance Criteria

- [ ] World sinh được customs/myths/cults rõ ràng.
- [ ] Era summaries tồn tại và dùng được cho agent context.
- [ ] Event log không phải nguồn context duy nhất cho mọi agent.
- [ ] Feed/timeline thể hiện được event loại culture/myth.

## Dependencies

- MVP path đã ổn định sau Sprint 06.
- Event/canonical layer đủ sạch để thêm depth.
- Team thống nhất format era summary.

## Sprint Task Board

| Task ID | Stream | Summary | Priority | Estimate |
| --- | --- | --- | --- | --- |
| ADW-S07-BA-01 | BA | Chốt acceptance criteria Culture/Myth và schema era summary | P1 | S |
| ADW-S07-BE-01 | Backend | Implement Culture Agent, Myth Agent và era summaries | P1 | XL |
| ADW-S07-FE-01 | Frontend | Hiển thị culture/myth tags và era summary panel | P2 | M |
| ADW-S07-DO-01 | DevOps | Theo dõi token cost và soak era transition | P2 | S |

## Risks & Control Notes

- Lore richness không có nghĩa nếu không queryable; summary và tags phải dùng được chứ không chỉ đẹp.
- Era summary dễ thành bản sao event log nếu không chốt rubric nén thông tin.
- Sprint này chỉ mở depth văn hóa/thần thoại, chưa chạm macro simulation rules.

## BA Checklist

- [ ] `BA-07.1` Chốt acceptance criteria cho Culture Agent.
- [ ] `BA-07.2` Chốt acceptance criteria cho Myth Agent.
- [ ] `BA-07.3` Chốt schema era summary và nghĩa của từng field.
- [ ] `BA-07.4` Tạo rubric review lore quality cho sprint này.
- [ ] `BA-07.5` Chốt semantics của event tagging cho culture/myth trên feed và timeline.
- [ ] `BA-07.6` Chuẩn bị demo path chứng minh world có bản sắc chứ không chỉ nhiều event.

## Backend Checklist

- [ ] `BE-07.1` Implement Culture Agent theo output contract đã chốt.
- [ ] `BE-07.2` Implement Myth Agent và link với civilization/religion context.
- [ ] `BE-07.3` Implement era summary generation sau các mốc history phù hợp.
- [ ] `BE-07.4` Implement summary storage/access để agent context không phụ thuộc event log thô.
- [ ] `BE-07.5` Link myths và culture markers vào canonical timeline/projections.
- [ ] `BE-07.6` Verify lore outputs đọc được, query được và dùng lại được trong runtime context.

## Frontend Checklist

- [ ] `FE-07.1` Hiển thị tags hoặc badges cho culture/myth events.
- [ ] `FE-07.2` Thêm era summary panel hoặc summary card trong luồng khám phá hiện tại.
- [ ] `FE-07.3` Bổ sung filter cho event types mới.
- [ ] `FE-07.4` Chuẩn bị data model cho Mythology Browser sprint sau.
- [ ] `FE-07.5` Verify summary panel không làm UI quá tải khi event volume lớn.
- [ ] `FE-07.6` Verify culture/myth labels dùng đúng vocabulary canon.

## DevOps Checklist

- [ ] `DO-07.1` Theo dõi token cost cho summary generation và myth/culture flows.
- [ ] `DO-07.2` Version config cho prompts và agent rules của sprint này.
- [ ] `DO-07.3` Thêm soak test vừa phải cho era transitions.
- [ ] `DO-07.4` Capture logs cho summary failures và malformed outputs.
- [ ] `DO-07.5` Chuẩn bị benchmark trước/sau khi dùng era summaries để đánh giá context savings.
- [ ] `DO-07.6` Verify summary generation path không làm build/demo profile mất ổn định.

## Demo & Sign-off

- Demo world có customs, myths, cults.
- Demo era summary được dùng lại làm context.
- [ ] Acceptance criteria được review đủ.
- [ ] Era summary đã đủ ngắn để tái sử dụng như context thay cho event log thô.
- [ ] Carry-over items được ghi lại sang Sprint 08 hoặc `MASTER-BACKLOG.md`.
- Sign-off owners: Product lead + runtime owner + BA.
