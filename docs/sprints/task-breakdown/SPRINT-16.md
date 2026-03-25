# Sprint 16 – Task Breakdown

## Breakdown Goal

Làm alternate timelines thành first-class world branches có provenance rõ ràng và compare UX đọc được.

## Work Packages

- `WP1` Fork and branch runtime
- `WP2` Divergence compare
- `WP3` Snapshot portability and ops

## Atomic Tasks

| ID | Parent | Stream | Task | Depends On | Output |
| --- | --- | --- | --- | --- | --- |
| T16-01 | ADW-S16-BA-01 | BA | Chốt branch provenance schema, compare projection shape và snapshot metadata | None | branch/snapshot contract |
| T16-02 | ADW-S16-BE-01 | Backend | Implement world forking tại year, era hoặc event checkpoint | T12-04,T16-01 | fork runtime |
| T16-03 | ADW-S16-BE-01 | Backend | Isolate mainline và branch trong runtime scheduling và state storage | T16-02 | branch isolation |
| T16-04 | ADW-S16-BE-01 | Backend | Build compare projections tóm tắt divergence thay vì raw diff thuần | T16-02,T16-03 | compare payload |
| T16-05 | ADW-S16-FE-01 | Frontend | Build fork flow từ timeline/checkpoint surfaces | T16-02 | fork UX |
| T16-06 | ADW-S16-FE-01 | Frontend | Build branch navigation và compare views | T16-04,T16-05 | branch compare UI |
| T16-07 | ADW-S16-FE-01 | Frontend | Build snapshot share/export states | T16-01,T16-06 | snapshot sharing UI |
| T16-08 | ADW-S16-DO-01 | DevOps | Define retention/cleanup policy cho branches và snapshots | T16-03,T16-07 | retention policy |
| T16-09 | ADW-S16-DO-01 | DevOps | Run restore drills và storage growth monitoring cho branch path | T16-08 | recovery/growth report |

## Suggested Sequence

1. `T16-01`
2. `T16-02 -> T16-03 -> T16-04`
3. `T16-05 -> T16-06 -> T16-07`
4. `T16-08 -> T16-09`

## Cut Line

- Must-have: `T16-01..T16-08`
- Can defer: `T16-09` growth modeling depth

## Verification Artifacts

- Branch diverge và tiếp tục independently
- Compare view giải thích được civilizations/regions/events changed
- Snapshot sharing portable và auditable
