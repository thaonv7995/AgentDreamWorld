# Sprint 10 – Mythology Browser & Knowledge Graph

## Sprint Metadata

| Field | Value |
| --- | --- |
| Phase | Phase 5 – Visualization |
| Milestone Gate | Gate F – Visualization Ready |
| Suggested Duration | 2 tuần |
| Primary Validation Signal | User đi qua được ít nhất một hành trình khám phá lore trọn vẹn qua browser và graph dữ liệu thật |
| Source Backlog IDs | `ADW-S10-BA-01`, `ADW-S10-BE-01`, `ADW-S10-FE-01`, `ADW-S10-DO-01` |

## Sprint Goal

Biến world thành hệ thống lore có thể khám phá theo entity graph.

## Business Objective

Mở rộng từ visualization không gian sang visualization quan hệ, để user khám phá thế giới theo cấu trúc lore thay vì chỉ timeline.

## Business Value

- Tăng chiều sâu khám phá world.
- Làm world có tính “wikiable” và “researchable” hơn.
- Hoàn thành visualization gate với layer lore relationship.

## In Scope

- Mythology Browser.
- Knowledge Graph beta.
- Entity link projections.
- Cross-navigation giữa graph/browser và feed/timeline/detail.

## Out of Scope

- Multi-world graph.
- Advanced social/community features.
- Full semantic search platform.
- Production-grade graph optimization beyond beta needs.

## Primary User Stories

- Với vai trò **writer/researcher**, tôi muốn duyệt myths, religions, events và civilizations theo quan hệ để hiểu lore nhanh hơn.
- Với vai trò **user tò mò**, tôi muốn click qua graph để khám phá world thay vì phải đọc hết timeline.
- Với vai trò **project lead**, tôi muốn xác nhận lore layer có thể scale beyond text list views.

## Acceptance Criteria

- [ ] Myths/religions/events/civilizations có thể được duyệt theo graph/browser.
- [ ] Graph dùng dữ liệu thật, không chỉ mock.
- [ ] Browser và graph link được sang detail/feed/timeline.
- [ ] User có thể theo ít nhất một path khám phá lore trọn vẹn.

## Dependencies

- Sprint 09 đã có projection pattern cho visualization.
- Sprint 07 đã có myth/culture foundation.
- Entity relationships trong backend đủ rõ để build graph.

## Sprint Task Board

| Task ID | Stream | Summary | Priority | Estimate |
| --- | --- | --- | --- | --- |
| ADW-S10-BA-01 | BA | Chốt taxonomy Mythology Browser và use cases Knowledge Graph | P1 | S |
| ADW-S10-BE-01 | Backend | Implement mythology projection và graph projection | P1 | L |
| ADW-S10-FE-01 | Frontend | Implement Mythology Browser và Knowledge Graph beta | P1 | XL |
| ADW-S10-DO-01 | DevOps | Theo dõi perf graph rendering và query latency | P2 | S |

## Risks & Control Notes

- Graph rất dễ trở thành visual noise nếu taxonomy và path khám phá không được chốt trước.
- Entity linking phải có giá trị điều hướng thật, không chỉ nối mọi thứ với mọi thứ.
- Đây là beta exploration layer; chưa tối ưu như một graph platform tổng quát.

## BA Checklist

- [ ] `BA-10.1` Chốt taxonomy cho Mythology Browser.
- [ ] `BA-10.2` Chốt use cases chính cho Knowledge Graph.
- [ ] `BA-10.3` Chốt acceptance criteria cho entity linking và relationship usefulness.
- [ ] `BA-10.4` Review cognitive load của graph UI để tránh visual overload.
- [ ] `BA-10.5` Chốt ít nhất một discovery path hoàn chỉnh mà user phải làm được.
- [ ] `BA-10.6` Chuẩn bị demo narrative cho visualization gate.

## Backend Checklist

- [ ] `BE-10.1` Implement mythology projection cho browser.
- [ ] `BE-10.2` Implement graph projection cho entity relationships.
- [ ] `BE-10.3` Link civilization, religion, myth, event, region, settlement theo model thật.
- [ ] `BE-10.4` Optimize query shape cho graph và browser.
- [ ] `BE-10.5` Verify graph data đủ để user follow ít nhất một lore path có nghĩa.
- [ ] `BE-10.6` Tạo sample response fixtures để frontend kiểm thử edge cases graph.

## Frontend Checklist

- [ ] `FE-10.1` Implement Mythology Browser cho taxonomy đã chốt.
- [ ] `FE-10.2` Implement Knowledge Graph beta cho exploration path chính.
- [ ] `FE-10.3` Implement cross-navigation từ graph/browser sang feed, timeline hoặc detail.
- [ ] `FE-10.4` Handle loading, empty và error states cho graph data nặng.
- [ ] `FE-10.5` Verify graph interactions không làm user mất context điều hướng.
- [ ] `FE-10.6` Verify browser và graph cùng dùng vocabulary canon của dự án.

## DevOps Checklist

- [ ] `DO-10.1` Theo dõi perf cho graph rendering và interaction path.
- [ ] `DO-10.2` Thêm profiling cho browser/query latency.
- [ ] `DO-10.3` Chuẩn bị visual regression và demo checklist cho graph/browser.
- [ ] `DO-10.4` Review export artifact compatibility với graph/browser data.
- [ ] `DO-10.5` Ghi lại benchmark frontend/runtime trước và sau khi thêm graph layer.
- [ ] `DO-10.6` Verify graph demo không phụ thuộc vào hidden local-only data patches.

## Demo & Sign-off

- Demo lore exploration theo graph và browser.
- [ ] Acceptance criteria được review đủ.
- [ ] Browser/graph link được sang feed, timeline hoặc detail view thật.
- [ ] Carry-over items được ghi lại sang Sprint 11 hoặc `MASTER-BACKLOG.md`.
- Sign-off owners: Product lead + frontend lead + backend lead.
