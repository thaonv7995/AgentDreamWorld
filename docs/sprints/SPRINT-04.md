# Sprint 04 – Dream Feed & World Overview UI

## Sprint Metadata

| Field | Value |
| --- | --- |
| Phase | Phase 2 – MVP Vertical Slice |
| Milestone Gate | Gate C – MVP Vertical Slice Ready |
| Suggested Duration | 2 tuần |
| Primary Validation Signal | User mở app và thấy Dream Feed cùng World Overview consume data thật, không dựa vào mock lâu dài |
| Source Backlog IDs | `ADW-S04-BA-01`, `ADW-S04-BE-01`, `ADW-S04-FE-01`, `ADW-S04-DO-01` |

## Sprint Goal

Người dùng bắt đầu quan sát được thế giới chạy qua UI usable đầu tiên.

## Business Objective

Biến data simulation thành trải nghiệm quan sát thực sự, để sản phẩm bắt đầu có UX thay vì chỉ là backend runtime. Dream Feed phải đọc như đang theo dõi lịch sử của một thế giới, không phải xem event log thô.

## Business Value

- Tạo vertical slice user-facing đầu tiên.
- Giảm rủi ro frontend đi lệch khỏi domain model.
- Chuẩn bị điều kiện để qua Gate C.

## In Scope

- Dream Feed UI.
- World Overview UI.
- Filter flow usable.
- Refresh/polling cơ bản.
- App shell nối API thật.

## Out of Scope

- Timeline hoàn chỉnh.
- God Mode.
- Map/graph visualization.
- Advanced styling hoặc AI visuals.

## Primary User Stories

- Với vai trò **user quan sát**, tôi muốn mở app và thấy lịch sử world đang hình thành theo thời gian.
- Với vai trò **user khám phá**, tôi muốn xem regions, civilizations và settlements từ world hiện tại.
- Với vai trò **team sản phẩm**, tôi muốn demo được một vertical slice nhìn thấy được cho MVP.

## Acceptance Criteria

- [ ] User mở app và thấy event feed thật.
- [ ] Dream Feed cards có `title + short narrative summary + tags`, không chỉ 1 dòng event khô.
- [ ] User xem được regions, civilizations, settlements trong World Overview.
- [ ] User filter được event theo các tiêu chí đã chốt.
- [ ] UI không còn phụ thuộc hoàn toàn vào mock data.
- [ ] Data hiển thị khớp với world summary và event API hiện tại.

## Dependencies

- Sprint 03 đã sinh được world và event data thật.
- API contract cho world/event đã ổn định tối thiểu.
- Team thống nhất information hierarchy cho observer-mode.

## Sprint Task Board

| Task ID | Stream | Summary | Priority | Estimate |
| --- | --- | --- | --- | --- |
| ADW-S04-BA-01 | BA | Chốt observer-mode UX, filter behavior và information hierarchy | P1 | S |
| ADW-S04-BE-01 | Backend | Tối ưu event/world queries cho vertical slice UI | P1 | M |
| ADW-S04-FE-01 | Frontend | Implement Dream Feed và World Overview UI | P1 | L |
| ADW-S04-DO-01 | DevOps | Thêm preview build và CI app-shell flow hỗ trợ demo | P2 | S |

## Risks & Control Notes

- UI không được đi nhanh hơn API tới mức phải sống bằng mock data thêm một sprint.
- Filter semantics phải khớp backend contract, nếu không sẽ gây drift sớm ở observer flow.
- Sprint này ưu tiên usable observer slice, chưa tối ưu visual depth hoặc advanced controls.

## BA Checklist

- [ ] `BA-04.1` Chốt observer-mode UX flow chính của V1 từ open app tới explore world.
- [ ] `BA-04.2` Chốt filter behavior cho feed, gồm default values và reset behavior.
- [ ] `BA-04.2b` Chốt rule copy cho Dream Feed: title ngan, summary 1-2 cau, factual-narrative.
- [ ] `BA-04.3` Chốt acceptance criteria cho World Overview: summary blocks nào bắt buộc, block nào defer.
- [ ] `BA-04.4` Review text labels và information hierarchy để thống nhất domain language trên UI.
- [ ] `BA-04.5` Chuẩn bị sample user journey cho demo Gate C.
- [ ] `BA-04.6` Chốt scope cut nếu UI đòi thêm visualization ngoài observer slice.

## Backend Checklist

- [ ] `BE-04.1` Tối ưu event list query cho feed theo response shape thực tế frontend cần.
- [ ] `BE-04.2` Tối ưu world summary query cho overview để tránh fetch thừa.
- [ ] `BE-04.3` Thêm response fields cần cho filter, `title`, `summary`, tags và metadata cards.
- [ ] `BE-04.4` Chốt pagination hoặc limit strategy cho feed.
- [ ] `BE-04.5` Verify semantics của filter ở API khớp acceptance criteria đã chốt.
- [ ] `BE-04.6` Chuẩn bị stable sample data path để frontend test observer flow.

## Frontend Checklist

- [ ] `FE-04.1` Implement Dream Feed UI với event cards, `title`, short narrative summary và meta structure rõ ràng.
- [ ] `FE-04.2` Implement tags/meta cho year, type, agent, civilization.
- [ ] `FE-04.3` Implement filter theo year, type, agent, civilization.
- [ ] `FE-04.4` Implement World Overview UI cho regions, civilizations, settlements.
- [ ] `FE-04.5` Implement polling/refresh strategy hoặc manual refresh path nhất quán.
- [ ] `FE-04.6` Verify UI hoạt động với data thật, gồm loading, empty và API error states.

## DevOps Checklist

- [ ] `DO-04.1` Thêm preview build cho frontend observer slice.
- [ ] `DO-04.2` Thêm CI build/check step cho app shell và API wiring.
- [ ] `DO-04.3` Kiểm tra env wiring giữa frontend và backend trên local và CI path.
- [ ] `DO-04.4` Ghi lại local runbook cho demo flow của Gate C.
- [ ] `DO-04.5` Chuẩn bị sample data snapshot để demo không lệ thuộc state ngẫu nhiên.
- [ ] `DO-04.6` Verify app shell end-to-end boot ổn định trên repo fresh clone.

## Demo & Sign-off

- Demo user journey: open app → xem Dream Feed → filter → xem World Overview.
- [ ] Acceptance criteria được review đủ.
- [ ] UI không còn phụ thuộc vào mock data cho luồng chính.
- [ ] Carry-over items được ghi lại sang Sprint 05 hoặc `MASTER-BACKLOG.md`.
- Sign-off owners: Product lead + frontend lead + BA.
