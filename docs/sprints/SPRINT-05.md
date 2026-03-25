# Sprint 05 – Timeline, Simulation Controls, God Mode Lite

## Sprint Metadata

| Field | Value |
| --- | --- |
| Phase | Phase 3 – MVP Release Candidate |
| Milestone Gate | Gate D – MVP Release Candidate |
| Suggested Duration | 2 tuần |
| Primary Validation Signal | User điều khiển simulation cơ bản và thấy timeline/god-mode tác động thật lên world state |
| Source Backlog IDs | `ADW-S05-BA-01`, `ADW-S05-BE-01`, `ADW-S05-FE-01`, `ADW-S05-DO-01` |

## Sprint Goal

Hoàn thiện trải nghiệm đọc lịch sử và can thiệp tối thiểu vào world.

## Business Objective

Mở rộng vertical slice MVP từ “xem feed” sang “đọc lịch sử” và “tác động có kiểm soát”, giúp sản phẩm gần hơn với core experience đã mô tả trong PRD.

## Business Value

- Tăng khả năng khám phá lịch sử của world.
- Thêm cơ chế tương tác tối thiểu để tạo hook trải nghiệm.
- Chuẩn bị điều kiện đi vào MVP release candidate.

## In Scope

- Timeline View.
- Simulation controls.
- God Mode lite.
- Better summaries cho world/era/civilization.

## Out of Scope

- God Mode nâng cao.
- Map và Civilization Viewer.
- Export artifacts.
- Full live mode controls phức tạp.

## Primary User Stories

- Với vai trò **user quan sát**, tôi muốn tua lại lịch sử của world thay vì chỉ xem feed hiện tại.
- Với vai trò **user thử nghiệm**, tôi muốn ném một sự kiện God Mode đơn giản để xem world phản ứng.
- Với vai trò **developer**, tôi muốn control simulation để debug world progression.

## Acceptance Criteria

- [ ] Timeline dùng được để đọc history.
- [ ] User có thể pause/resume/manual tick.
- [ ] God Mode preset tạo hậu quả hợp lệ trong world state.
- [ ] Timeline và feed phản ánh cùng một canonical history.
- [ ] Guardian validate được God Mode events.

## Dependencies

- Sprint 04 đã có UI vertical slice.
- Event timeline projection đã đủ dùng.
- Summary model đủ ổn định để hiển thị ở UI.

## Sprint Task Board

| Task ID | Stream | Summary | Priority | Estimate |
| --- | --- | --- | --- | --- |
| ADW-S05-BA-01 | BA | Chốt UX timeline và preset God Mode V1 | P1 | S |
| ADW-S05-BE-01 | Backend | Implement timeline projection, controls và God Mode lite endpoints | P1 | L |
| ADW-S05-FE-01 | Frontend | Implement Timeline UI, simulation controls và God Mode lite panel | P1 | L |
| ADW-S05-DO-01 | DevOps | Chuẩn bị staging/demo profile cho timeline và God Mode | P2 | S |

## Risks & Control Notes

- God Mode rất dễ kéo scope sang sandbox/game editor; chỉ cho phép preset interventions đã chốt.
- Timeline zoom/range semantics phải ổn định để không làm lệch mental model của user.
- Controls phải tác động lên state thật; không chấp nhận demo chỉ thay UI local state.

## BA Checklist

- [ ] `BA-05.1` Chốt UX timeline navigation: default range, zoom behavior và transition path từ feed.
- [ ] `BA-05.2` Chốt 1-2 preset God Mode cho V1 cùng semantics và giới hạn rõ ràng.
- [ ] `BA-05.3` Chốt acceptance criteria cho pause, resume và manual tick.
- [ ] `BA-05.4` Chốt rule hậu quả tối thiểu của God Mode và cách user nhận biết impact.
- [ ] `BA-05.5` Chuẩn bị demo scenarios cho timeline, controls và God Mode.
- [ ] `BA-05.6` Review non-goals để không trượt sang editor/sandbox product.

## Backend Checklist

- [ ] `BE-05.1` Implement timeline query/projection đủ cho UI đọc history theo range.
- [ ] `BE-05.2` Implement pause, resume và manual tick controls ở backend.
- [ ] `BE-05.3` Implement God Mode lite endpoints cho các preset đã chốt.
- [ ] `BE-05.4` Improve world, era và civilization summaries cho timeline/detail usage.
- [ ] `BE-05.5` Ensure Guardian validate được God Mode events và reject invalid interventions.
- [ ] `BE-05.6` Verify timeline/feed phản ánh cùng một canonical history sau interventions.

## Frontend Checklist

- [ ] `FE-05.1` Implement Timeline View usable cho reading history.
- [ ] `FE-05.2` Implement zoom/range controls cơ bản và current selection state.
- [ ] `FE-05.3` Implement simulation controls UI cho pause, resume và manual tick.
- [ ] `FE-05.4` Implement God Mode lite panel cho preset actions.
- [ ] `FE-05.5` Hiển thị hậu quả event sau trigger trên feed/timeline.
- [ ] `FE-05.6` Verify control states, loading states và error handling không làm lệch world state view.

## DevOps Checklist

- [ ] `DO-05.1` Tạo staging/demo profile cho timeline và God Mode.
- [ ] `DO-05.2` Thêm seed/demo commands cho replay ổn định của same world history.
- [ ] `DO-05.3` Theo dõi errors và latency cho control endpoints.
- [ ] `DO-05.4` Thêm smoke checks cho pause/resume/manual tick path.
- [ ] `DO-05.5` Chuẩn bị release checklist đầu vào cho MVP RC phase.
- [ ] `DO-05.6` Verify demo path có thể lặp lại mà không cần thao tác tay ngoài docs.

## Demo & Sign-off

- Demo timeline navigation.
- Demo God Mode preset và hậu quả trên feed/timeline.
- [ ] Acceptance criteria được review đủ.
- [ ] Timeline và controls tác động lên world state thật.
- [ ] Carry-over items được ghi lại sang Sprint 06 hoặc `MASTER-BACKLOG.md`.
- Sign-off owners: Product lead + backend lead + frontend lead.
