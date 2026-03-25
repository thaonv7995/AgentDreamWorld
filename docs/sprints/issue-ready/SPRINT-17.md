# Sprint 17 – Issue-Ready Board

## Suggested Order

`EP-S17-01` -> `EP-S17-02` -> `EP-S17-03`

## Epic `EP-S17-01` – Provider/Profile Resolution

- [ ] Epic complete

### Issue `ADW-S17-BA-01` – Runtime config contract

- [ ] Issue complete
- Depends on: `ADW-S16-BA-01`
- Subtasks:
  - [ ] `T17-01` Chốt provider/profile config schema, runtime inspection payload và local health contract

### Issue `ADW-S17-BE-01` – Provider routing backend

- [ ] Issue complete
- Depends on: `T11-02`, `T17-01`
- Subtasks:
  - [ ] `T17-02` Resolve config ở global và agent-group level
  - [ ] `T17-03` Keep cloud provider adapters dưới cùng `AgentModel` contract
  - [ ] `T17-04` Add local provider path với health check và fallback semantics

## Epic `EP-S17-02` – Runtime Inspection UX

- [ ] Epic complete

### Issue `ADW-S17-FE-01` – Provider settings và inspection UI

- [ ] Issue complete
- Depends on: `T17-03`, `T17-04`
- Subtasks:
  - [ ] `T17-05` Build settings UI cho provider/profile selection
  - [ ] `T17-06` Build runtime profile inspection view cho active world

## Epic `EP-S17-03` – Multi-provider Operations

- [ ] Epic complete

### Issue `ADW-S17-DO-01` – Provider ops matrix

- [ ] Issue complete
- Depends on: `T17-04`, `T17-06`
- Subtasks:
  - [ ] `T17-07` Run provider smoke matrix với ít nhất 2 cloud và 1 local path
  - [ ] `T17-08` Review secrets/config handling và write local provider setup notes

## Verification Checklist

- [ ] Ít nhất 2 cloud và 1 local path chạy được
- [ ] Fallback behavior visible và understandable
- [ ] Default config flow vẫn tối giản cho non-advanced users
