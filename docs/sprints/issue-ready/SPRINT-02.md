# Sprint 02 – Issue-Ready Board

## Suggested Order

`EP-S02-01` -> `EP-S02-02` -> `EP-S02-03`

## Epic `EP-S02-01` – Tick Orchestration

- [ ] Epic complete

### Issue `ADW-S02-BA-01` – Event lifecycle contract

- [ ] Issue complete
- Depends on: `ADW-S01-BA-01`
- Subtasks:
  - [ ] `T02-01` Chốt event lifecycle và raw/canonical semantics

### Issue `ADW-S02-BE-01` – Tick orchestration baseline

- [ ] Issue complete
- Depends on: `T02-01`
- Subtasks:
  - [ ] `T02-02` Implement `EventProposal` + append-only event log path
  - [ ] `T02-03` Implement manual tick orchestrator

## Epic `EP-S02-02` – Guardian/Historian Baseline

- [ ] Epic complete

### Issue `ADW-S02-BE-01` – Validation and canonicalization

- [ ] Issue complete
- Depends on: `T02-01`, `T02-03`
- Subtasks:
  - [ ] `T02-04` Implement declarative Guardian rule loader/validators
  - [ ] `T02-05` Implement scoring Historian canonicalization

### Issue `ADW-S02-FE-01` – Debug tick UI

- [ ] Issue complete
- Depends on: `T02-03`
- Subtasks:
  - [ ] `T02-08` Build debug tick trigger + event list shell

## Epic `EP-S02-03` – Observability & Replay

- [ ] Epic complete

### Issue `ADW-S02-BE-01` – Observability tables and mock path

- [ ] Issue complete
- Depends on: `T02-03`
- Subtasks:
  - [ ] `T02-06` Add `llm_call_log`, `tick_log`, `PipelineStage` tagging
  - [ ] `T02-07` Add `MockAgentModel` + replay-ready fixture path

### Issue `ADW-S02-DO-01` – Tick smoke and reporting

- [ ] Issue complete
- Depends on: `T02-06`, `T02-07`
- Subtasks:
  - [ ] `T02-09` Add timeout/retry/report/smoke for tick lifecycle

## Verification Checklist

- [ ] Manual tick succeeds in mock mode
- [ ] `report --last N` shows success/reject/cost/latency
- [ ] Guardian reject reasons visible
