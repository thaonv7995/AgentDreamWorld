# Sprint 13 – Issue-Ready Board

## Suggested Order

`EP-S13-01` -> `EP-S13-02` -> `EP-S13-03`

## Epic `EP-S13-01` – World Lifecycle API

- [ ] Epic complete

### Issue `ADW-S13-BA-01` – Lifecycle contract

- [ ] Issue complete
- Depends on: `ADW-S12-BA-01`
- Subtasks:
  - [ ] `T13-01` Chốt lifecycle state machine, preset metadata schema và switching acceptance criteria

### Issue `ADW-S13-BE-01` – World lifecycle backend

- [ ] Issue complete
- Depends on: `T12-05`, `T13-01`
- Subtasks:
  - [ ] `T13-02` Build create/select/archive world lifecycle APIs
  - [ ] `T13-03` Persist world presets thành data thay vì implicit UI naming
  - [ ] `T13-04` Protect active runtime jobs khi switching current world

## Epic `EP-S13-02` – World Manager UX

- [ ] Epic complete

### Issue `ADW-S13-FE-01` – Multi-world manager UI

- [ ] Issue complete
- Depends on: `T13-02`, `T13-03`, `T13-04`
- Subtasks:
  - [ ] `T13-05` Build world manager shell và list states
  - [ ] `T13-06` Build create world flow với preset selection
  - [ ] `T13-07` Build select/switch/archive UX cho empty, single và multi-world cases

## Epic `EP-S13-03` – Multi-world Smoke & Storage Hygiene

- [ ] Epic complete

### Issue `ADW-S13-DO-01` – Multi-world operations

- [ ] Issue complete
- Depends on: `T13-07`
- Subtasks:
  - [ ] `T13-08` Smoke create/select/archive flows trên 2–3 worlds
  - [ ] `T13-09` Review storage growth và align backup naming theo `world_id`

## Verification Checklist

- [ ] 2–3 worlds coexist và switch cleanly
- [ ] Switching không leak feed/config/state
- [ ] Single-world path vẫn đơn giản với user bình thường
