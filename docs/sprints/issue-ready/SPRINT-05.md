# Sprint 05 – Issue-Ready Board

## Suggested Order

`EP-S05-01` -> `EP-S05-02` -> `EP-S05-03`

## Epic `EP-S05-01` – Timeline Projection

- [ ] Epic complete

### Issue `ADW-S05-BA-01` – Timeline and God Mode lite semantics

- [ ] Issue complete
- Depends on: `ADW-S04-BA-01`
- Subtasks:
  - [ ] `T05-01` Chốt UX timeline và preset God Mode semantics

### Issue `ADW-S05-BE-01` – Timeline read model

- [ ] Issue complete
- Depends on: `T04-02`, `T05-01`
- Subtasks:
  - [ ] `T05-02` Build timeline projection/grouping

### Issue `ADW-S05-FE-01` – Timeline UI

- [ ] Issue complete
- Depends on: `T05-02`
- Subtasks:
  - [ ] `T05-05` Implement timeline UI and navigation states

## Epic `EP-S05-02` – Simulation Controls

- [ ] Epic complete

### Issue `ADW-S05-BE-01` – Control state machine

- [ ] Issue complete
- Depends on: `T02-03`, `T05-01`
- Subtasks:
  - [ ] `T05-03` Implement pause/resume/manual tick controls

### Issue `ADW-S05-FE-01` – Controls UI

- [ ] Issue complete
- Depends on: `T05-03`, `T05-04`
- Subtasks:
  - [ ] `T05-06` Implement simulation controls + preset panel

## Epic `EP-S05-03` – God Mode Lite

- [ ] Epic complete

### Issue `ADW-S05-BE-01` – Preset interventions

- [ ] Issue complete
- Depends on: `T05-03`, `T05-01`
- Subtasks:
  - [ ] `T05-04` Implement preset intervention endpoints

### Issue `ADW-S05-DO-01` – Demo profile

- [ ] Issue complete
- Depends on: `T05-05`, `T05-06`
- Subtasks:
  - [ ] `T05-07` Add demo/staging profile for timeline and controls

## Verification Checklist

- [ ] Timeline navigation works
- [ ] Pause/resume/manual tick safe
- [ ] Preset intervention visible in timeline/feed
