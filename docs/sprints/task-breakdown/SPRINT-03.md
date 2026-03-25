# Sprint 03 – Task Breakdown

## Breakdown Goal

Sinh world đầu tiên bằng 3 creative agents V1 và khóa API contracts trước Sprint 04.

## Work Packages

- `WP1` Genesis runtime
- `WP2` API/projection contract
- `WP3` Replay/snapshot confidence

## Atomic Tasks

| ID | Parent | Stream | Task | Depends On | Output |
| --- | --- | --- | --- | --- | --- |
| T03-01 | ADW-S03-BA-01 | BA | Chốt genesis acceptance criteria và output rubric | None | genesis rubric |
| T03-02 | ADW-S03-BE-01 | Backend | Implement Creator agent V1 | T02-07 | creator path |
| T03-03 | ADW-S03-BE-01 | Backend | Implement Civilization agent V1 | T02-07 | civ path |
| T03-04 | ADW-S03-BE-01 | Backend | Implement Storyteller agent V1 | T02-07 | storyteller path |
| T03-05 | ADW-S03-BE-01 | Backend | Implement genesis runner with boundaries | T03-02,T03-03,T03-04 | genesis runtime |
| T03-06 | ADW-S03-BA-01 | BA | Chốt feed/timeline projection contract | T03-01 | projection contract |
| T03-07 | ADW-S03-BE-01 | Backend | Expose filterable events/world summary APIs | T03-05,T03-06 | real API data |
| T03-08 | ADW-S03-BE-01 | Backend | Add TypeScript contract types + contract tests | T03-07 | stable contract |
| T03-09 | ADW-S03-BE-01 | Backend | Add snapshot/replay tests cho genesis path | T03-05,T03-07 | deterministic checks |
| T03-10 | ADW-S03-FE-01 | Frontend | Build genesis progress + feed/overview shell from real API | T03-07,T03-08 | UI shell |
| T03-11 | ADW-S03-DO-01 | DevOps | Add mock/live profiles and genesis smoke path | T03-09 | smoke/demo profile |

## Suggested Sequence

1. `T03-01`
2. `T03-02..T03-04`
3. `T03-05`
4. `T03-06 -> T03-07 -> T03-08`
5. `T03-09`
6. `T03-10 -> T03-11`

## Cut Line

- Must-have: `T03-01..T03-09`
- Can defer: `T03-10` polish depth

## Verification Artifacts

- Genesis produces non-empty world in scope
- Contract tests pass
- Snapshot replay stable
