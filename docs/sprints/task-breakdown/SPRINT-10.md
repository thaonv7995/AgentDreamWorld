# Sprint 10 – Task Breakdown

## Breakdown Goal

Biến world thành linked lore system với Mythology Browser và Knowledge Graph beta có giá trị khám phá thực.

## Work Packages

- `WP1` Entity linking and graph projection
- `WP2` Lore browser and graph UI
- `WP3` Linked export and performance safety

## Atomic Tasks

| ID | Parent | Stream | Task | Depends On | Output |
| --- | --- | --- | --- | --- | --- |
| T10-01 | ADW-S10-BA-01 | BA | Chốt graph node/edge taxonomy, mythology browser categories và linked export semantics | None | graph/browser contract |
| T10-02 | ADW-S10-BE-01 | Backend | Build entity linking pipeline giữa civ, myth, event, region và settlement | T09-04,T09-05,T10-01 | linked entities |
| T10-03 | ADW-S10-BE-01 | Backend | Build graph-friendly node/edge projections có explainable source links | T10-02 | graph projection |
| T10-04 | ADW-S10-BE-01 | Backend | Implement browser/query APIs với safe bounds cho V2 world size | T10-03 | lore query API |
| T10-05 | ADW-S10-BE-01 | Backend | Extend export pipeline để preserve linked relationships | T10-03,T10-04 | linked export path |
| T10-06 | ADW-S10-FE-01 | Frontend | Build Mythology Browser views và category navigation | T10-04 | mythology browser UI |
| T10-07 | ADW-S10-FE-01 | Frontend | Build Knowledge Graph beta với safe defaults và filters | T10-03,T10-04 | graph explorer UI |
| T10-08 | ADW-S10-FE-01 | Frontend | Add cross-navigation giữa graph, timeline, map và civ detail | T10-06,T10-07 | linked navigation UX |
| T10-09 | ADW-S10-DO-01 | DevOps | Measure graph query latency/render perf và prepare dense-link sample worlds | T10-05,T10-08 | graph perf report |

## Suggested Sequence

1. `T10-01`
2. `T10-02 -> T10-03 -> T10-04`
3. `T10-05`
4. `T10-06` + `T10-07`
5. `T10-08 -> T10-09`

## Cut Line

- Must-have: `T10-01..T10-08`
- Can defer: `T10-09` performance investigation depth

## Verification Artifacts

- Graph usable ở target V2 world size
- Mythology Browser link tới entities/events thật
- Linked export giữ được quan hệ cốt lõi
