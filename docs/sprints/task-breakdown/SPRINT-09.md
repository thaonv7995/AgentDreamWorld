# Sprint 09 – Task Breakdown

## Breakdown Goal

Chuyển sang geography-first exploration với map beta và civilization viewer dùng projection thật.

## Work Packages

- `WP1` Spatial projections
- `WP2` Map and civ surfaces
- `WP3` Visual quality and performance

## Atomic Tasks

| ID | Parent | Stream | Task | Depends On | Output |
| --- | --- | --- | --- | --- | --- |
| T09-01 | ADW-S09-BA-01 | BA | Chốt map projection shape, civ payload và ownership semantics | None | map/civ contract |
| T09-02 | ADW-S09-BE-01 | Backend | Build region/world map projection từ world model hiện có | T08-05,T09-01 | map projection |
| T09-03 | ADW-S09-BE-01 | Backend | Build territory ownership projection | T09-02 | ownership data |
| T09-04 | ADW-S09-BE-01 | Backend | Build civilization detail read model với history và settlement summaries | T09-01,T09-03 | civ detail payload |
| T09-05 | ADW-S09-BE-01 | Backend | Add settlement distribution summary cho map/civ surfaces | T09-02,T09-04 | settlement distribution data |
| T09-06 | ADW-S09-FE-01 | Frontend | Render map beta từ projection thật | T09-02,T09-03 | map beta UI |
| T09-07 | ADW-S09-FE-01 | Frontend | Build Civilization Viewer và navigation từ feed/timeline sang civ detail | T09-04,T09-06 | civ viewer UI |
| T09-08 | ADW-S09-FE-01 | Frontend | Handle sparse-world fallback states và empty geography gracefully | T09-06,T09-07 | robust edge-state UX |
| T09-09 | ADW-S09-DO-01 | DevOps | Set perf budget cho map rendering, visual QA snapshots và spatially diverse seeds | T09-05,T09-08 | visual/perf baseline |

## Suggested Sequence

1. `T09-01`
2. `T09-02 -> T09-03`
3. `T09-04 -> T09-05`
4. `T09-06 -> T09-07 -> T09-08`
5. `T09-09`

## Cut Line

- Must-have: `T09-01..T09-08`
- Can defer: `T09-09` snapshot coverage depth

## Verification Artifacts

- Map render được nhiều world không cần tweak tay
- Civilization Viewer khớp backend state
- Feed -> civ -> map navigation chạy thông
