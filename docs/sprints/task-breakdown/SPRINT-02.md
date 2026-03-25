# Sprint 02 – Task Breakdown

## Breakdown Goal

Tạo tick pipeline end-to-end có observability baseline, deterministic mock path và rule engine nền.

## Work Packages

- `WP1` Tick orchestration
- `WP2` Guardian/Historian baseline
- `WP3` Observability and replay

## Atomic Tasks

| ID | Parent | Stream | Task | Depends On | Output |
| --- | --- | --- | --- | --- | --- |
| T02-01 | ADW-S02-BA-01 | BA | Chốt event lifecycle và raw/canonical semantics | None | lifecycle contract |
| T02-02 | ADW-S02-BE-01 | Backend | Implement `EventProposal` + append-only event log path | T02-01 | proposal pipeline |
| T02-03 | ADW-S02-BE-01 | Backend | Implement manual tick orchestrator | T02-02 | tick endpoint |
| T02-04 | ADW-S02-BE-01 | Backend | Implement declarative Guardian rule loader/validators | T02-01,T02-03 | guardian baseline |
| T02-05 | ADW-S02-BE-01 | Backend | Implement scoring Historian canonicalization | T02-01,T02-03 | historian baseline |
| T02-06 | ADW-S02-BE-01 | Backend | Add `llm_call_log`, `tick_log`, `PipelineStage` tagging | T02-03 | observability tables |
| T02-07 | ADW-S02-BE-01 | Backend | Add `MockAgentModel` + replay-ready fixture path | T02-03 | deterministic mock path |
| T02-08 | ADW-S02-FE-01 | Frontend | Build debug tick trigger + event list shell | T02-03 | debug UI |
| T02-09 | ADW-S02-DO-01 | DevOps | Add timeout/retry/report/smoke for tick lifecycle | T02-06,T02-07 | report + smoke |

## Suggested Sequence

1. `T02-01`
2. `T02-02 -> T02-03`
3. `T02-04` + `T02-05`
4. `T02-06 -> T02-07`
5. `T02-08` + `T02-09`

## Cut Line

- Must-have: `T02-01..T02-07`
- Can defer: `T02-08`

## Verification Artifacts

- Manual tick succeeds in mock mode
- `report --last N` shows success/reject/cost/latency
- Guardian reject reasons visible
