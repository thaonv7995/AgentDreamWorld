# Sprint 01 – Task Breakdown

## Breakdown Goal

Khóa schema V1 và persistence layer cho world model 7 core tables.

## Work Packages

- `WP1` Canon schema
- `WP2` Repository/read model
- `WP3` Seed and smoke path

## Atomic Tasks

| ID | Parent | Stream | Task | Depends On | Output |
| --- | --- | --- | --- | --- | --- |
| T01-01 | ADW-S01-BA-01 | BA | Chốt glossary entity V1 và response contract `GET /worlds/current` | None | canon glossary |
| T01-02 | ADW-S01-BE-01 | Backend | Tạo migrations cho `worlds, regions, locations, civilizations, settlements, events, eras` | T01-01 | schema v1 |
| T01-03 | ADW-S01-BE-01 | Backend | Implement DB init + schema version tracking | T01-02 | init flow |
| T01-04 | ADW-S01-BE-01 | Backend | Implement database-per-world path resolution | T01-02 | `data/world-{name}.db` |
| T01-05 | ADW-S01-BE-01 | Backend | Implement repositories cho world summary + events read path | T01-03 | repo layer |
| T01-06 | ADW-S01-BE-01 | Backend | Tạo seed world không dùng LLM | T01-05 | persisted seed |
| T01-07 | ADW-S01-FE-01 | Frontend | Tạo world summary types và overview shell | T01-01,T01-06 | overview shell |
| T01-08 | ADW-S01-DO-01 | DevOps | Smoke test DB init/restart/seed path | T01-06 | smoke check |

## Suggested Sequence

1. `T01-01`
2. `T01-02 -> T01-03 -> T01-04`
3. `T01-05 -> T01-06`
4. `T01-07 -> T01-08`

## Cut Line

- Must-have: `T01-01..T01-06`
- Can defer: `T01-07`

## Verification Artifacts

- Seed world readable after restart
- `GET /worlds/current` returns real data
