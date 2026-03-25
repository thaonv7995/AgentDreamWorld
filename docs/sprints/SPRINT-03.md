# Sprint 03 – Genesis Mode & 3 Creative Agents V1

## Sprint Metadata

| Field | Value |
| --- | --- |
| Phase | Phase 2 – MVP Vertical Slice |
| Milestone Gate | Gate C – MVP Vertical Slice Ready |
| Suggested Duration | 2 tuần |
| Primary Validation Signal | Genesis tạo ra world không rỗng, nằm trong boundaries V1 và đọc được qua API |
| Source Backlog IDs | `ADW-S03-BA-01`, `ADW-S03-BE-01`, `ADW-S03-FE-01`, `ADW-S03-DO-01` |

## Sprint Goal

Tạo được world đầu tiên bằng Genesis mode với 3 creative agents của V1.

## Business Objective

Chứng minh AI Dreams World có thể tự sinh một thế giới đầu tiên đủ giàu để bắt đầu quan sát, thay vì chỉ có pipeline kỹ thuật rỗng.

## Business Value

- Tạo “first magic moment” của sản phẩm.
- Mở đường cho Dream Feed và World Overview dùng dữ liệu thật.
- Xác nhận scope V1 có thể sinh ra world đủ có nghĩa trong giới hạn đã chốt.

## In Scope

- Creator Agent V1.
- Civilization Agent V1.
- Storyteller Agent V1.
- Genesis mode 50–200 ticks.
- Simulation boundaries config.
- Event listing/filter API.

## Out of Scope

- Culture/Myth/Ecology/Economy/Chaos.
- Timeline UI hoàn chỉnh.
- God Mode.
- Map và graph visualization.

## Primary User Stories

- Với vai trò **user quan sát**, tôi muốn thấy một world đầu tiên tự sinh ra từ hư không để cảm nhận được giá trị cốt lõi của sản phẩm.
- Với vai trò **developer**, tôi muốn API trả về world và event data thật sau genesis để có thể dựng UI thật.
- Với vai trò **product lead**, tôi muốn xác nhận 3 creative agents V1 đủ tạo vertical slice đầu tiên.

## Acceptance Criteria

- [ ] World sau genesis không còn rỗng.
- [ ] Có 3–4 regions.
- [ ] Có civilizations và settlements đầu tiên.
- [ ] Event list API filter được theo year/type/agent/civilization.
- [ ] Simulation boundaries được áp dụng, không vượt scope V1 đã khóa.

## Dependencies

- Sprint 02 đã có tick pipeline hoạt động.
- World model và event model đã ổn định.
- Mock/live model strategy đã rõ ràng.

## Sprint Task Board

| Task ID | Stream | Summary | Priority | Estimate |
| --- | --- | --- | --- | --- |
| ADW-S03-BA-01 | BA | Chốt acceptance criteria Genesis và quality rubric cho 3 creative agents V1 | P1 | S |
| ADW-S03-BE-01 | Backend | Implement Creator, Civilization, Storyteller và Genesis runner | P1 | XL |
| ADW-S03-FE-01 | Frontend | Render world/event data thật sau Genesis với loading/filter shell | P2 | M |
| ADW-S03-DO-01 | DevOps | Thiết lập provider profiles, retry/timeout và smoke Genesis run | P2 | M |

## Risks & Control Notes

- Agent prompts có thể tạo world vượt scope V1 nếu boundaries không được enforce ngay trong runner.
- Cost/latency của Genesis dễ tăng đột biến; phải giữ mock/live profile rõ ràng.
- Không thêm agent V2 trong sprint này dù có chỗ trống kỹ thuật.

## BA Checklist

- [ ] `BA-03.1` Chốt acceptance criteria cho Genesis mode theo đúng boundaries V1.
- [ ] `BA-03.2` Chốt dữ liệu tối thiểu phải có sau Genesis: regions, civilizations, settlements, event volume cơ bản.
- [ ] `BA-03.3` Chốt output quality rubric cho Creator, Civilization và Storyteller.
- [ ] `BA-03.4` Chốt filter contract cho event API: year, type, agent, civilization.
- [ ] `BA-03.5` Chốt rule active-agents-per-tick và các hard limits phải enforce trong runner.
- [ ] `BA-03.6` Chuẩn bị demo script và sign-off questions cho “first magic moment”.

## Backend Checklist

- [ ] `BE-03.1` Implement Creator Agent V1 theo output contract đã chốt.
- [ ] `BE-03.2` Implement Civilization Agent V1 và link với seed world structure.
- [ ] `BE-03.3` Implement Storyteller Agent V1 cho event generation path trong Genesis.
- [ ] `BE-03.4` Implement Genesis mode runner cho 50-200 ticks.
- [ ] `BE-03.5` Áp simulation boundaries vào world bootstrap để không vượt V1 scope.
- [ ] `BE-03.6` Expose event list/filter API với dữ liệu thật sau Genesis.
- [ ] `BE-03.7` Persist world summaries và verify post-genesis state đọc lại được sau restart.

## Frontend Checklist

- [ ] `FE-03.1` Tạo Genesis progress/loading state đủ rõ cho run kéo dài.
- [ ] `FE-03.2` Render event feed data thật từ API sau khi Genesis hoàn tất.
- [ ] `FE-03.3` Render world summary cards cho regions, civilizations và settlements đầu tiên.
- [ ] `FE-03.4` Thêm filter UI skeleton cho event list theo contract đã chốt.
- [ ] `FE-03.5` Xử lý empty/error/retry states cho Genesis flow.
- [ ] `FE-03.6` Verify số lượng hiển thị khớp với boundaries world thật sau Genesis.

## DevOps Checklist

- [ ] `DO-03.1` Thiết lập secrets path cho provider và policy local env an toàn.
- [ ] `DO-03.2` Tạo local profile `mock` và `live` với switch rõ ràng.
- [ ] `DO-03.3` Thiết lập retry, timeout và failure logging cho provider calls.
- [ ] `DO-03.4` Thêm smoke run cho Genesis mode ở profile `mock`.
- [ ] `DO-03.5` Ghi lại metric runtime cơ bản: total duration, failure count, output size.
- [ ] `DO-03.6` Chuẩn bị command/demo profile để Genesis run có thể lặp lại ổn định.

## Demo & Sign-off

- Demo run genesis và show world đầu tiên hình thành.
- Demo event feed data thật sau genesis.
- [ ] Acceptance criteria được review đủ.
- [ ] World sau Genesis nằm trong scope `3–4 regions`, `3–6 civilizations`, `<=20 settlements`.
- [ ] Carry-over items được ghi lại sang Sprint 04 hoặc `MASTER-BACKLOG.md`.
- Sign-off owners: Product lead + backend lead + BA.
