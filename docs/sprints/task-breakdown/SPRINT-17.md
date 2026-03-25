# Sprint 17 – Task Breakdown

## Breakdown Goal

Hoàn tất runtime flexibility với multi-provider và local LLM như các path được support chính thức.

## Work Packages

- `WP1` Provider/profile resolution
- `WP2` Runtime inspection UX
- `WP3` Multi-provider operations

## Atomic Tasks

| ID | Parent | Stream | Task | Depends On | Output |
| --- | --- | --- | --- | --- | --- |
| T17-01 | ADW-S17-BA-01 | BA | Chốt provider/profile config schema, runtime inspection payload và local health contract | None | runtime config contract |
| T17-02 | ADW-S17-BE-01 | Backend | Resolve config ở global và agent-group level | T11-02,T17-01 | hierarchical config resolver |
| T17-03 | ADW-S17-BE-01 | Backend | Keep cloud provider adapters dưới cùng `AgentModel` contract | T17-02 | provider adapter layer |
| T17-04 | ADW-S17-BE-01 | Backend | Add local provider path với health check và fallback semantics | T17-02,T17-03 | local runtime path |
| T17-05 | ADW-S17-FE-01 | Frontend | Build settings UI cho provider/profile selection | T17-03,T17-04 | runtime settings UI |
| T17-06 | ADW-S17-FE-01 | Frontend | Build runtime profile inspection view cho active world | T17-01,T17-05 | runtime inspection UI |
| T17-07 | ADW-S17-DO-01 | DevOps | Run provider smoke matrix với ít nhất 2 cloud và 1 local path | T17-04,T17-06 | provider smoke matrix |
| T17-08 | ADW-S17-DO-01 | DevOps | Review secrets/config handling và write local provider setup notes | T17-07 | multi-provider ops note |

## Suggested Sequence

1. `T17-01`
2. `T17-02 -> T17-03 -> T17-04`
3. `T17-05 -> T17-06`
4. `T17-07 -> T17-08`

## Cut Line

- Must-have: `T17-01..T17-07`
- Can defer: `T17-08` documentation polish

## Verification Artifacts

- Ít nhất 2 cloud và 1 local path chạy được
- Fallback behavior visible và understandable
- Default config flow vẫn tối giản cho non-advanced users
