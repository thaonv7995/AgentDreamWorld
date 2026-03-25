# Sprint 11 – Optional Advanced Infra & Observability

## Sprint Metadata

| Field | Value |
| --- | --- |
| Phase | Phase 6 – Platform Expansion |
| Milestone Gate | Gate G – Platform Expansion Ready |
| Suggested Duration | 2 tuần |
| Primary Validation Signal | Advanced profile và observability path hoạt động như option mà không làm thay đổi default SQLite flow |
| Source Backlog IDs | `ADW-S11-BA-01`, `ADW-S11-BE-01`, `ADW-S11-FE-01`, `ADW-S11-DO-01` |

## Sprint Goal

Chuẩn bị đường scale nâng cao mà không làm vỡ default SQLite path.

## Business Objective

Thêm khả năng quan sát và profile nâng cao để dự án có đường phát triển dài hạn, nhưng không phá trải nghiệm cài đặt đơn giản của MVP/V2.

## Business Value

- Chuẩn bị scale path.
- Tăng khả năng đo chi phí và độ ổn định.
- Tạo nền cho contributor/profile deploy phức tạp hơn.

## In Scope

- Optional Postgres profile.
- Optional Redis profile.
- Observability dashboard hoặc metrics path.
- Perf/load baseline.

## Out of Scope

- Bắt buộc chuyển sang Postgres/Redis.
- Full cloud deployment stack.
- Multi-world production operations hoàn chỉnh.
- Re-architect toàn bộ runtime.

## Primary User Stories

- Với vai trò **operator/maintainer**, tôi muốn theo dõi tick health, cost và reject rate.
- Với vai trò **advanced contributor**, tôi muốn chạy hệ thống theo profile nâng cao nếu cần.
- Với vai trò **project lead**, tôi muốn có dữ liệu thật để quyết định có nên scale infra hay không.

## Acceptance Criteria

- [ ] SQLite vẫn là default path.
- [ ] Advanced profile chạy như lựa chọn, không ép buộc.
- [ ] Metrics đủ để theo dõi tick health và cost.
- [ ] Perf/load baseline được ghi nhận thành tài liệu.

## Dependencies

- MVP/V2 path phải ổn định trước khi mở advanced profile.
- Config system phải đủ rõ để hỗ trợ nhiều mode.
- Team thống nhất observability scope tối thiểu.

## Sprint Task Board

| Task ID | Stream | Summary | Priority | Estimate |
| --- | --- | --- | --- | --- |
| ADW-S11-BA-01 | BA | Chốt non-goals và KPI/SLI cho advanced profile | P2 | S |
| ADW-S11-BE-01 | Backend | Tách config profile và expose instrumentation layer | P1 | L |
| ADW-S11-FE-01 | Frontend | Thêm admin/debug health summary tối thiểu | P2 | S |
| ADW-S11-DO-01 | DevOps | Thiết lập compose advanced profile và observability baseline | P1 | L |

## Risks & Control Notes

- Optional infra không được trở thành prerequisite ngầm cho contributor mới.
- Observability phải đủ để ra quyết định, không phải mở một stack ops quá nặng cho nhu cầu hiện tại.
- Mọi thay đổi config profile phải giữ SQLite-first làm đường mặc định rõ ràng.

## BA Checklist

- [ ] `BA-11.1` Chốt non-goals cho advanced profile để giữ SQLite-first path.
- [ ] `BA-11.2` Chốt KPI và SLI cần quan sát trong advanced profile.
- [ ] `BA-11.3` Chốt acceptance criteria cho optional profile và debug health view.
- [ ] `BA-11.4` Review release impact để không trượt V1/V2 path.
- [ ] `BA-11.5` Chốt decision points: khi nào advanced infra được xem là cần thiết thật.
- [ ] `BA-11.6` Chuẩn bị demo script cho default path vs advanced path comparison.

## Backend Checklist

- [ ] `BE-11.1` Tách config cho SQLite và Postgres profile mà không đổi default path.
- [ ] `BE-11.2` Thêm optional Redis hooks, cache hoặc queue path ở mức foundation.
- [ ] `BE-11.3` Expose metrics endpoint hoặc instrumentation layer.
- [ ] `BE-11.4` Verify compatibility của simulation engine trên nhiều profile.
- [ ] `BE-11.5` Thêm fallback defaults để app vẫn chạy nếu advanced profile không được bật.
- [ ] `BE-11.6` Ghi lại config contract cho DevOps và contributors nâng cao.

## Frontend Checklist

- [ ] `FE-11.1` Tạo admin hoặc debug panel tối thiểu cho health metrics nếu cần.
- [ ] `FE-11.2` Hiển thị runtime health summary ở chế độ debug.
- [ ] `FE-11.3` Giữ production user UI không bị nhiễu bởi ops concerns.
- [ ] `FE-11.4` Feature-gate toàn bộ advanced/debug UI rõ ràng.
- [ ] `FE-11.5` Verify default user path không thấy advanced profile complexity.
- [ ] `FE-11.6` Verify debug panel đọc đúng metrics thật, không chỉ mock values.

## DevOps Checklist

- [ ] `DO-11.1` Tạo `docker-compose` hoặc local stack cho advanced profile.
- [ ] `DO-11.2` Thiết lập observability stack tối thiểu cho metrics/logs cần thiết.
- [ ] `DO-11.3` Chạy load hoặc perf test cơ bản cho advanced profile.
- [ ] `DO-11.4` Thiết lập backup/restore baseline cho data profiles.
- [ ] `DO-11.5` Chuẩn bị runbook bật/tắt advanced profile mà không ảnh hưởng default path.
- [ ] `DO-11.6` Verify contributor mới vẫn đi được default SQLite flow mà không cần stack nâng cao.

## Demo & Sign-off

- Demo default SQLite path vẫn chạy.
- Demo advanced profile và metrics path như option.
- [ ] Acceptance criteria được review đủ.
- [ ] Default SQLite path vẫn là luồng cài đặt và chạy chính.
- [ ] Carry-over items được ghi lại sang Sprint 12 hoặc `MASTER-BACKLOG.md`.
- Sign-off owners: Project lead + DevOps lead + backend lead.
