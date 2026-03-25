# Sprint 13 – Task Breakdown

## Breakdown Goal

Biến multi-world foundation thành product UX usable với happy path ngắn cho create/select/archive world.

## Work Packages

- `WP1` World lifecycle API
- `WP2` World manager UX
- `WP3` Multi-world smoke and storage hygiene

## Atomic Tasks

| ID | Parent | Stream | Task | Depends On | Output |
| --- | --- | --- | --- | --- | --- |
| T13-01 | ADW-S13-BA-01 | BA | Chốt lifecycle state machine, preset metadata schema và switching acceptance criteria | None | lifecycle contract |
| T13-02 | ADW-S13-BE-01 | Backend | Build create/select/archive world lifecycle APIs | T12-05,T13-01 | lifecycle API |
| T13-03 | ADW-S13-BE-01 | Backend | Persist world presets thành data thay vì implicit UI naming | T13-01,T13-02 | preset persistence |
| T13-04 | ADW-S13-BE-01 | Backend | Protect active runtime jobs khi switching current world | T13-02 | safe switching runtime |
| T13-05 | ADW-S13-FE-01 | Frontend | Build world manager shell và list states | T13-02 | world manager UI |
| T13-06 | ADW-S13-FE-01 | Frontend | Build create world flow với preset selection | T13-03,T13-05 | create flow |
| T13-07 | ADW-S13-FE-01 | Frontend | Build select/switch/archive UX cho empty, single và multi-world cases | T13-04,T13-05 | switching UX |
| T13-08 | ADW-S13-DO-01 | DevOps | Smoke create/select/archive flows trên 2–3 worlds | T13-07 | multi-world smoke report |
| T13-09 | ADW-S13-DO-01 | DevOps | Review storage growth và align backup naming theo `world_id` | T13-08 | world_id-aligned ops note |

## Suggested Sequence

1. `T13-01`
2. `T13-02 -> T13-03 -> T13-04`
3. `T13-05 -> T13-06 -> T13-07`
4. `T13-08 -> T13-09`

## Cut Line

- Must-have: `T13-01..T13-08`
- Can defer: `T13-09` storage analysis depth

## Verification Artifacts

- 2–3 worlds coexist và switch cleanly
- Switching không leak feed/config/state
- Single-world path vẫn đơn giản với user bình thường
