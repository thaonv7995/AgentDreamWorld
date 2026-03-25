# Sprint 11 – Task Breakdown

## Breakdown Goal

Thêm advanced profile và advanced observability mà vẫn giữ SQLite-first default path là source of truth chuẩn.

## Work Packages

- `WP1` Profile resolution
- `WP2` Advanced telemetry surfaces
- `WP3` Ops baseline for optional infra

## Atomic Tasks

| ID | Parent | Stream | Task | Depends On | Output |
| --- | --- | --- | --- | --- | --- |
| T11-01 | ADW-S11-BA-01 | BA | Chốt profile selection semantics, metrics naming và SQLite-first guarantee | None | profile/metrics contract |
| T11-02 | ADW-S11-BE-01 | Backend | Refactor config/profile resolution thành path rõ ràng cho default và advanced profile | T11-01 | profile resolver |
| T11-03 | ADW-S11-BE-01 | Backend | Add optional Postgres profile | T11-02 | postgres profile |
| T11-04 | ADW-S11-BE-01 | Backend | Add optional Redis hooks cho advanced runtime paths | T11-02 | redis integration hooks |
| T11-05 | ADW-S11-BE-01 | Backend | Implement advanced metrics/trace/export surfaces reusing `tick_log` và `llm_call_log` | T11-02 | advanced telemetry layer |
| T11-06 | ADW-S11-FE-01 | Frontend | Build minimal feature-gated admin health summary | T11-05 | admin health UI |
| T11-07 | ADW-S11-DO-01 | DevOps | Prepare compose stack cho advanced profile | T11-03,T11-04,T11-05 | optional infra stack |
| T11-08 | ADW-S11-DO-01 | DevOps | Run load baseline, backup/restore checks và document perf notes | T11-07 | perf and recovery baseline |
| T11-09 | ADW-S11-DO-01 | DevOps | Verify default SQLite path vẫn chạy độc lập và không phụ thuộc advanced stack | T11-05,T11-08 | default-path verification |

## Suggested Sequence

1. `T11-01`
2. `T11-02`
3. `T11-03` + `T11-04` + `T11-05`
4. `T11-06`
5. `T11-07 -> T11-08 -> T11-09`

## Cut Line

- Must-have: `T11-01..T11-06,T11-09`
- Can defer: `T11-07..T11-08` tooling polish depth

## Verification Artifacts

- Default path vẫn chạy khi không có advanced stack
- Advanced profile dùng lại baseline truths thay vì tạo telemetry truth mới
- Perf/load notes đủ để ra quyết định scale về sau
