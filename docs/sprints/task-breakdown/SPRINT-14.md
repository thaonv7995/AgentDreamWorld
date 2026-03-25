# Sprint 14 – Task Breakdown

## Breakdown Goal

Bổ sung control và inspection surfaces để vận hành multi-world product an toàn theo từng world riêng biệt.

## Work Packages

- `WP1` Pace and fast-forward control
- `WP2` Inspectability surfaces
- `WP3` Runtime and cost validation

## Atomic Tasks

| ID | Parent | Stream | Task | Depends On | Output |
| --- | --- | --- | --- | --- | --- |
| T14-01 | ADW-S14-BA-01 | BA | Chốt pace semantics, fast-forward bounds, log payload và config inspector schema | None | control/inspect contract |
| T14-02 | ADW-S14-BE-01 | Backend | Add per-world pace state machine | T13-04,T14-01 | pace runtime |
| T14-03 | ADW-S14-BE-01 | Backend | Implement bounded fast-forward orchestration reusing tick pipeline | T14-02 | fast-forward path |
| T14-04 | ADW-S14-BE-01 | Backend | Build Event Log Viewer read model với filters và pagination | T14-01,T14-03 | log viewer API |
| T14-05 | ADW-S14-BE-01 | Backend | Build Config Inspector read model và per-world runtime status payload | T14-01,T14-02 | config/runtime payload |
| T14-06 | ADW-S14-FE-01 | Frontend | Build control surfaces cho pace và fast-forward | T14-03 | pace control UI |
| T14-07 | ADW-S14-FE-01 | Frontend | Build Event Log Viewer UI | T14-04 | log viewer UI |
| T14-08 | ADW-S14-FE-01 | Frontend | Build Config Inspector/debug panel | T14-05 | config inspector UI |
| T14-09 | ADW-S14-DO-01 | DevOps | Run soak tests theo từng pace mode | T14-03,T14-08 | pace soak report |
| T14-10 | ADW-S14-DO-01 | DevOps | Compare cost/latency giữa normal và fast-forward, verify metrics reflect control state | T14-09 | control-state ops report |

## Suggested Sequence

1. `T14-01`
2. `T14-02 -> T14-03`
3. `T14-04` + `T14-05`
4. `T14-06 -> T14-07 -> T14-08`
5. `T14-09 -> T14-10`

## Cut Line

- Must-have: `T14-01..T14-09`
- Can defer: `T14-10` comparative analysis depth

## Verification Artifacts

- Fast-forward tạo state transitions coherent
- Logs/config hiển thị là real và current
- Operator inspect được world mà không phải chạm DB/files
