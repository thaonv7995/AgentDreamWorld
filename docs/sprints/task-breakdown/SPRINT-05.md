# Sprint 05 – Task Breakdown

## Breakdown Goal

Hoàn thiện lịch sử có thể điều hướng và intervention tối thiểu qua timeline + God Mode lite.

## Work Packages

- `WP1` Timeline projection
- `WP2` Simulation controls
- `WP3` God Mode lite

## Atomic Tasks

| ID | Parent | Stream | Task | Depends On | Output |
| --- | --- | --- | --- | --- | --- |
| T05-01 | ADW-S05-BA-01 | BA | Chốt UX timeline và preset God Mode semantics | None | control contract |
| T05-02 | ADW-S05-BE-01 | Backend | Build timeline projection/grouping | T04-02,T05-01 | timeline read model |
| T05-03 | ADW-S05-BE-01 | Backend | Implement pause/resume/manual tick controls | T02-03,T05-01 | control state machine |
| T05-04 | ADW-S05-BE-01 | Backend | Implement preset intervention endpoints | T05-03,T05-01 | God Mode lite |
| T05-05 | ADW-S05-FE-01 | Frontend | Implement timeline UI and navigation states | T05-02 | timeline UI |
| T05-06 | ADW-S05-FE-01 | Frontend | Implement simulation controls + preset panel | T05-03,T05-04 | control UI |
| T05-07 | ADW-S05-DO-01 | DevOps | Add demo/staging profile for timeline and controls | T05-05,T05-06 | demo profile |

## Suggested Sequence

1. `T05-01`
2. `T05-02` + `T05-03`
3. `T05-04`
4. `T05-05` + `T05-06`
5. `T05-07`

## Cut Line

- Must-have: `T05-01..T05-06`
- Can defer: `T05-07`

## Verification Artifacts

- Timeline navigation works
- Pause/resume/manual tick safe
- Preset intervention visible in timeline/feed
