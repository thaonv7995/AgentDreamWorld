# Sprint 04 – Task Breakdown

## Breakdown Goal

Đưa user vào observer mode với Dream Feed và World Overview đọc dữ liệu thật.

## Work Packages

- `WP1` Observer read models
- `WP2` Feed UI
- `WP3` Overview UI and refresh path

## Atomic Tasks

| ID | Parent | Stream | Task | Depends On | Output |
| --- | --- | --- | --- | --- | --- |
| T04-01 | ADW-S04-BA-01 | BA | Chốt information hierarchy và filter behavior | None | observer UX contract |
| T04-02 | ADW-S04-BE-01 | Backend | Optimize feed queries and filters | T03-07,T04-01 | feed read model |
| T04-03 | ADW-S04-BE-01 | Backend | Optimize world summary/overview queries | T03-07,T04-01 | overview read model |
| T04-04 | ADW-S04-FE-01 | Frontend | Implement Dream Feed cards/filter states | T04-02 | feed UI |
| T04-05 | ADW-S04-FE-01 | Frontend | Implement World Overview panels/cards | T04-03 | overview UI |
| T04-06 | ADW-S04-FE-01 | Frontend | Add polling/refresh and stale/error states | T04-04,T04-05 | refresh path |
| T04-07 | ADW-S04-DO-01 | DevOps | Add preview build and demo smoke checks | T04-04,T04-05 | preview/demo path |

## Suggested Sequence

1. `T04-01`
2. `T04-02` + `T04-03`
3. `T04-04` + `T04-05`
4. `T04-06`
5. `T04-07`

## Cut Line

- Must-have: `T04-01..T04-06`
- Can defer: `T04-07`

## Verification Artifacts

- Feed and overview show real data
- Refresh path updates without corruption
