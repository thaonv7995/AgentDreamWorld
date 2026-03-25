# Sprint 04 – Issue-Ready Board

## Suggested Order

`EP-S04-01` -> `EP-S04-02` -> `EP-S04-03`

## Epic `EP-S04-01` – Observer Read Models

- [ ] Epic complete

### Issue `ADW-S04-BA-01` – Observer UX contract

- [ ] Issue complete
- Depends on: `ADW-S03-BA-01`
- Subtasks:
  - [ ] `T04-01` Chốt information hierarchy và filter behavior

### Issue `ADW-S04-BE-01` – Feed/overview read models

- [ ] Issue complete
- Depends on: `T03-07`, `T04-01`
- Subtasks:
  - [ ] `T04-02` Optimize feed queries and filters
  - [ ] `T04-03` Optimize world summary/overview queries

## Epic `EP-S04-02` – Feed UI

- [ ] Epic complete

### Issue `ADW-S04-FE-01` – Dream Feed UI

- [ ] Issue complete
- Depends on: `T04-02`
- Subtasks:
  - [ ] `T04-04` Implement Dream Feed cards/filter states

## Epic `EP-S04-03` – Overview UI & Refresh Path

- [ ] Epic complete

### Issue `ADW-S04-FE-01` – Overview and refresh states

- [ ] Issue complete
- Depends on: `T04-03`
- Subtasks:
  - [ ] `T04-05` Implement World Overview panels/cards
  - [ ] `T04-06` Add polling/refresh and stale/error states

### Issue `ADW-S04-DO-01` – Preview/demo path

- [ ] Issue complete
- Depends on: `T04-04`, `T04-05`
- Subtasks:
  - [ ] `T04-07` Add preview build and demo smoke checks

## Verification Checklist

- [ ] Feed and overview show real data
- [ ] Refresh path updates without corruption
