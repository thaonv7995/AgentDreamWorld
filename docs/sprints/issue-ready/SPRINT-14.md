# Sprint 14 – Issue-Ready Board

## Suggested Order

`EP-S14-01` -> `EP-S14-02` -> `EP-S14-03`

## Epic `EP-S14-01` – Pace & Fast-Forward Control

- [ ] Epic complete

### Issue `ADW-S14-BA-01` – Control/inspect contract

- [ ] Issue complete
- Depends on: `ADW-S13-BA-01`
- Subtasks:
  - [ ] `T14-01` Chốt pace semantics, fast-forward bounds, log payload và config inspector schema

### Issue `ADW-S14-BE-01` – Per-world control runtime

- [ ] Issue complete
- Depends on: `T13-04`, `T14-01`
- Subtasks:
  - [ ] `T14-02` Add per-world pace state machine
  - [ ] `T14-03` Implement bounded fast-forward orchestration reusing tick pipeline

### Issue `ADW-S14-FE-01` – Pace controls UI

- [ ] Issue complete
- Depends on: `T14-03`
- Subtasks:
  - [ ] `T14-06` Build control surfaces cho pace và fast-forward

## Epic `EP-S14-02` – Inspectability Surfaces

- [ ] Epic complete

### Issue `ADW-S14-BE-01` – Log/config projections

- [ ] Issue complete
- Depends on: `T14-01`, `T14-03`
- Subtasks:
  - [ ] `T14-04` Build Event Log Viewer read model với filters và pagination
  - [ ] `T14-05` Build Config Inspector read model và per-world runtime status payload

### Issue `ADW-S14-FE-01` – Viewer/inspector UI

- [ ] Issue complete
- Depends on: `T14-04`, `T14-05`
- Subtasks:
  - [ ] `T14-07` Build Event Log Viewer UI
  - [ ] `T14-08` Build Config Inspector/debug panel

## Epic `EP-S14-03` – Runtime & Cost Validation

- [ ] Epic complete

### Issue `ADW-S14-DO-01` – Pace verification flow

- [ ] Issue complete
- Depends on: `T14-03`, `T14-08`
- Subtasks:
  - [ ] `T14-09` Run soak tests theo từng pace mode
  - [ ] `T14-10` Compare cost/latency giữa normal và fast-forward, verify metrics reflect control state

## Verification Checklist

- [ ] Fast-forward tạo state transitions coherent
- [ ] Logs/config hiển thị là real và current
- [ ] Operator inspect được world mà không phải chạm DB/files
