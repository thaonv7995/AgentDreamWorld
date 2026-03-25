# Sprint 09 – Region Map & Civilization Viewer

## Sprint Metadata

| Field | Value |
| --- | --- |
| Phase | Phase 5 – Visualization |
| Milestone Gate | Gate F – Visualization Ready |
| Suggested Duration | 2 tuần |
| Primary Validation Signal | User khám phá được world qua map và civ detail bằng dữ liệu thật, không hard-code theo một world mẫu |
| Source Backlog IDs | `ADW-S09-BA-01`, `ADW-S09-BE-01`, `ADW-S09-FE-01`, `ADW-S09-DO-01` |

## Sprint Goal

Nâng trải nghiệm từ text-first sang exploration trực quan hơn.

## Business Objective

Cho user nhìn thấy cấu trúc không gian và chi tiết civilization một cách trực quan, để product bắt đầu có feel của một world exploration system chứ không chỉ là event reader.

## Business Value

- Tăng khả năng khám phá world.
- Làm data model trở nên dễ hiểu hơn với user không kỹ thuật.
- Mở nền cho visualization gate.

## In Scope

- Region/world map beta.
- Civilization Viewer.
- Territory ownership projection.
- Settlement distribution view.

## Out of Scope

- Knowledge Graph.
- Mythology Browser hoàn chỉnh.
- 3D map hoặc layout procedural phức tạp.
- Multi-world UX.

## Primary User Stories

- Với vai trò **user khám phá**, tôi muốn nhìn thấy world trên map để hiểu geography và ownership.
- Với vai trò **user theo dõi lore**, tôi muốn xem chi tiết một civilization ở một màn hình riêng.
- Với vai trò **product lead**, tôi muốn chứng minh data model hiện tại đủ mạnh để dựng visualization thực.

## Acceptance Criteria

- [ ] Map dùng dữ liệu thật từ world model.
- [ ] Civilization Viewer đọc được history/geography/summary thật.
- [ ] Layout không hard-code cho từng world.
- [ ] User có thể chuyển từ event/civ summary sang civ detail.

## Dependencies

- Sprint 08 đã ổn định post-MVP simulation depth.
- Có đủ projection data cho regions, settlements, territory ownership.
- Frontend shell đủ vững để mở thêm view phức tạp.

## Sprint Task Board

| Task ID | Stream | Summary | Priority | Estimate |
| --- | --- | --- | --- | --- |
| ADW-S09-BA-01 | BA | Chốt UX map beta và content bắt buộc của Civilization Viewer | P1 | S |
| ADW-S09-BE-01 | Backend | Implement map projection, territory ownership và civ detail projection | P1 | L |
| ADW-S09-FE-01 | Frontend | Implement map beta và Civilization Viewer | P1 | XL |
| ADW-S09-DO-01 | DevOps | Thiết lập perf budget và preview deployment cho visual QA | P2 | S |

## Risks & Control Notes

- Visualization không được bù đắp bằng hard-code nếu projection data còn thiếu; phải lộ rõ gap thật.
- Map readability quan trọng hơn visual complexity; không làm procedural layout phức tạp ở sprint này.
- Perf budget phải được theo dõi từ đầu, tránh để graph/map cùng lúc làm vỡ frontend shell.

## BA Checklist

- [ ] `BA-09.1` Chốt UX cho map beta, gồm entry point và expected navigation path.
- [ ] `BA-09.2` Chốt nội dung bắt buộc của Civilization Viewer.
- [ ] `BA-09.3` Chốt definition cho territory và ownership display.
- [ ] `BA-09.4` Review acceptance criteria cho map readability và detail usefulness.
- [ ] `BA-09.5` Chốt cách user đi từ feed/timeline sang civ detail và ngược lại.
- [ ] `BA-09.6` Chuẩn bị demo script chứng minh map không chỉ là visual decoration.

## Backend Checklist

- [ ] `BE-09.1` Implement map projection data shape cho regions và settlements.
- [ ] `BE-09.2` Implement territory ownership projection.
- [ ] `BE-09.3` Implement civilization detail endpoint hoặc projection.
- [ ] `BE-09.4` Expose settlement distribution data cho map/civ detail.
- [ ] `BE-09.5` Verify projection data không hard-code theo một world mẫu.
- [ ] `BE-09.6` Tạo sample projection fixtures để frontend và QA dùng chung.

## Frontend Checklist

- [ ] `FE-09.1` Implement map beta shell và interaction flow tối thiểu.
- [ ] `FE-09.2` Render regions và settlements từ projection data thật.
- [ ] `FE-09.3` Render territory ownership bằng visual encoding đủ rõ.
- [ ] `FE-09.4` Implement Civilization Viewer cho history, geography, summary.
- [ ] `FE-09.5` Link feed/timeline items sang civ detail.
- [ ] `FE-09.6` Verify loading/error/perf states cho map và civ detail path.

## DevOps Checklist

- [ ] `DO-09.1` Thiết lập perf budget cho map rendering và civ detail page.
- [ ] `DO-09.2` Thêm preview deployment cho visual QA.
- [ ] `DO-09.3` Theo dõi frontend bundle impact và asset growth.
- [ ] `DO-09.4` Chuẩn bị demo datasets hoặc world snapshots cho map.
- [ ] `DO-09.5` Tạo checklist visual QA cho readability trên desktop/mobile.
- [ ] `DO-09.6` Verify map demo chạy ổn định với dữ liệu thật và sample snapshot.

## Demo & Sign-off

- Demo user khám phá world qua map và civ detail.
- [ ] Acceptance criteria được review đủ.
- [ ] Map và Civilization Viewer dùng dữ liệu thật từ projection layer.
- [ ] Carry-over items được ghi lại sang Sprint 10 hoặc `MASTER-BACKLOG.md`.
- Sign-off owners: Product lead + frontend lead + BA.
