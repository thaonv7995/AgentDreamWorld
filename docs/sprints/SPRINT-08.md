# Sprint 08 – Ecology, Economy, Chaos, Macro Rules

## Sprint Metadata

| Field | Value |
| --- | --- |
| Phase | Phase 4 – Expanded Simulation |
| Milestone Gate | Gate E – Expanded Simulation Ready |
| Suggested Duration | 2 tuần |
| Primary Validation Signal | Macro rules làm tăng depth simulation nhưng tick success và coherence vẫn giữ trong ngưỡng chấp nhận |
| Source Backlog IDs | `ADW-S08-BA-01`, `ADW-S08-BE-01`, `ADW-S08-FE-01`, `ADW-S08-DO-01` |

## Sprint Goal

Mở rộng simulation theo hướng macro sâu hơn nhưng vẫn giữ coherence.

## Business Objective

Tăng độ phong phú và tính emergent của world mà không phá vỡ readability và narrative physics đã chốt cho V1/V2.

## Business Value

- Làm thế giới bớt tuyến tính và ít lặp hơn.
- Tạo chain reaction giữa ecology, economy, chaos.
- Chuẩn bị điều kiện qua Gate E.

## In Scope

- Ecology Agent.
- Economy Agent.
- Chaos Agent.
- Scarcity/conflict propagation rules.
- Guardian rules mở rộng cho V2 simulation.
- Metrics theo dõi reject rate và instability.

## Out of Scope

- Visualization nâng cao.
- Mythology Browser.
- Graph explorer.
- Multi-world support.

## Primary User Stories

- Với vai trò **user quan sát**, tôi muốn thế giới phản ứng dây chuyền một cách có nghĩa khi tài nguyên khan hiếm hoặc thảm họa xảy ra.
- Với vai trò **runtime owner**, tôi muốn mở thêm agents mà vẫn giữ được coherence.
- Với vai trò **project lead**, tôi muốn expanded simulation nhưng không đánh đổi readability.

## Acceptance Criteria

- [ ] Event variety tăng nhưng world không bị loạn.
- [ ] Guardian kiểm soát được invalid rate ở ngưỡng chấp nhận.
- [ ] Ecology/economy/chaos tạo được hậu quả liên hoàn có nghĩa.
- [ ] Simulation boundaries vẫn giữ world trong phạm vi readable.

## Dependencies

- Sprint 07 đã có era summaries và richer lore foundation.
- Guardian baseline đã đủ để mở rộng.
- Observability tối thiểu có thể đo reject/tick behavior.

## Sprint Task Board

| Task ID | Stream | Summary | Priority | Estimate |
| --- | --- | --- | --- | --- |
| ADW-S08-BA-01 | BA | Chốt macro rules và coherence metrics cho expanded simulation | P1 | S |
| ADW-S08-BE-01 | Backend | Implement Ecology, Economy, Chaos và propagation rules | P1 | XL |
| ADW-S08-FE-01 | Frontend | Mở rộng feed/timeline cho event types và impact labels mới | P2 | S |
| ADW-S08-DO-01 | DevOps | Chạy long-run simulation test và theo dõi budget/reject rate | P1 | M |

## Risks & Control Notes

- Macro rules dễ tạo chain reaction hấp dẫn nhưng vô nghĩa; Guardian và metrics phải bắt được điều đó.
- Nếu tick duration hoặc reject rate tăng mạnh, phải cắt bớt rule complexity thay vì cố giữ full scope.
- Expanded simulation vẫn phải readable; không đánh đổi clarity để lấy số lượng event.

## BA Checklist

- [ ] `BA-08.1` Chốt macro rules cho ecology, economy và chaos theo đúng boundary expanded simulation.
- [ ] `BA-08.2` Chốt acceptance criteria cho scarcity/conflict chains và chain reaction có nghĩa.
- [ ] `BA-08.3` Chốt metric theo dõi coherence, reject rate và readability.
- [ ] `BA-08.4` Review risk của scope creep vượt V2 boundary.
- [ ] `BA-08.5` Chuẩn bị sample scenarios cho disaster, scarcity, trade disruption và recovery.
- [ ] `BA-08.6` Chốt điều kiện fail-fast nếu simulation trở nên quá loạn hoặc quá đắt.

## Backend Checklist

- [ ] `BE-08.1` Implement Ecology Agent theo rules đã chốt.
- [ ] `BE-08.2` Implement Economy Agent và các drivers scarcity/trade.
- [ ] `BE-08.3` Implement Chaos Agent cho disaster/anomaly/conflict escalation path.
- [ ] `BE-08.4` Implement scarcity/conflict propagation rules giữa regions, civilizations và settlements.
- [ ] `BE-08.5` Mở rộng Guardian rules cho V2 event classes.
- [ ] `BE-08.6` Tune simulation boundaries để giữ world readable và tick success rate chấp nhận được.
- [ ] `BE-08.7` Verify ít nhất một chain reaction đi trọn từ nguyên nhân -> hậu quả -> canonical summary.

## Frontend Checklist

- [ ] `FE-08.1` Hiển thị event types mới trong feed và timeline.
- [ ] `FE-08.2` Bổ sung summary hoặc impact labels cho ecology, economy, chaos events.
- [ ] `FE-08.3` Thêm filter cho scarcity, disaster và trade events.
- [ ] `FE-08.4` Chuẩn bị visual states cho map impacts ở sprint sau.
- [ ] `FE-08.5` Verify expanded event volume vẫn readable trong UI hiện tại.
- [ ] `FE-08.6` Verify labels/filter không làm user nhầm macro event với lore/culture event.

## DevOps Checklist

- [ ] `DO-08.1` Thêm metrics cho tick duration, reject rate và chain-reaction error patterns.
- [ ] `DO-08.2` Chạy long-run simulation test cho expanded simulation profile.
- [ ] `DO-08.3` Theo dõi budget per tick sau khi mở thêm agents/rules.
- [ ] `DO-08.4` Tạo alert/log review checklist cho simulation instability.
- [ ] `DO-08.5` Ghi lại benchmark trước/sau khi thêm macro rules.
- [ ] `DO-08.6` Verify long-run test artifacts đủ để project lead review coherence risk.

## Demo & Sign-off

- Demo ecology/economy/chaos events tạo chain reaction nhưng vẫn coherent.
- [ ] Acceptance criteria được review đủ.
- [ ] Coherence metrics và reject-rate review đã được ghi lại.
- [ ] Carry-over items được ghi lại sang Sprint 09 hoặc `MASTER-BACKLOG.md`.
- Sign-off owners: Runtime owner + backend lead + project lead.
