# Sprint 11 – Issue-Ready Board

## Suggested Order

`EP-S11-01` -> `EP-S11-02` -> `EP-S11-03`

## Epic `EP-S11-01` – Profile Resolution

- [ ] Epic complete

### Issue `ADW-S11-BA-01` – Profile and metrics contract

- [ ] Issue complete
- Depends on: `ADW-S10-BA-01`
- Subtasks:
  - [ ] `T11-01` Chốt profile selection semantics, metrics naming và SQLite-first guarantee

### Issue `ADW-S11-BE-01` – Config/profile resolver

- [ ] Issue complete
- Depends on: `T11-01`
- Subtasks:
  - [ ] `T11-02` Refactor config/profile resolution thành path rõ ràng cho default và advanced profile

## Epic `EP-S11-02` – Advanced Telemetry Surfaces

- [ ] Epic complete

### Issue `ADW-S11-BE-01` – Optional infra hooks và advanced telemetry

- [ ] Issue complete
- Depends on: `T11-02`
- Subtasks:
  - [ ] `T11-03` Add optional Postgres profile
  - [ ] `T11-04` Add optional Redis hooks cho advanced runtime paths
  - [ ] `T11-05` Implement advanced metrics/trace/export surfaces reusing `tick_log` và `llm_call_log`

### Issue `ADW-S11-FE-01` – Minimal admin health UI

- [ ] Issue complete
- Depends on: `T11-05`
- Subtasks:
  - [ ] `T11-06` Build minimal feature-gated admin health summary

## Epic `EP-S11-03` – Ops Baseline for Optional Infra

- [ ] Epic complete

### Issue `ADW-S11-DO-01` – Advanced profile operations

- [ ] Issue complete
- Depends on: `T11-03`, `T11-04`, `T11-05`
- Subtasks:
  - [ ] `T11-07` Prepare compose stack cho advanced profile
  - [ ] `T11-08` Run load baseline, backup/restore checks và document perf notes
  - [ ] `T11-09` Verify default SQLite path vẫn chạy độc lập và không phụ thuộc advanced stack

## Verification Checklist

- [ ] Default path vẫn chạy khi không có advanced stack
- [ ] Advanced profile dùng lại baseline truths thay vì tạo telemetry truth mới
- [ ] Perf/load notes đủ để ra quyết định scale về sau
