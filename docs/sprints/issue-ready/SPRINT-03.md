# Sprint 03 – Issue-Ready Board

## Suggested Order

`EP-S03-01` -> `EP-S03-02` -> `EP-S03-03`

## Epic `EP-S03-01` – Genesis Runtime

- [ ] Epic complete

### Issue `ADW-S03-BA-01` – Genesis rubric

- [ ] Issue complete
- Depends on: `ADW-S02-BA-01`
- Subtasks:
  - [ ] `T03-01` Chốt genesis acceptance criteria và output rubric

### Issue `ADW-S03-BE-01` – 3 creative agents và runner

- [ ] Issue complete
- Depends on: `T02-07`
- Subtasks:
  - [ ] `T03-02` Implement Creator agent V1
  - [ ] `T03-03` Implement Civilization agent V1
  - [ ] `T03-04` Implement Storyteller agent V1
  - [ ] `T03-05` Implement genesis runner with boundaries

## Epic `EP-S03-02` – API & Projection Contract

- [ ] Epic complete

### Issue `ADW-S03-BA-01` – Projection contract

- [ ] Issue complete
- Depends on: `T03-01`
- Subtasks:
  - [ ] `T03-06` Chốt feed/timeline projection contract

### Issue `ADW-S03-BE-01` – Real API data contract

- [ ] Issue complete
- Depends on: `T03-05`, `T03-06`
- Subtasks:
  - [ ] `T03-07` Expose filterable events/world summary APIs
  - [ ] `T03-08` Add TypeScript contract types + contract tests

### Issue `ADW-S03-FE-01` – Genesis UI shell

- [ ] Issue complete
- Depends on: `T03-07`, `T03-08`
- Subtasks:
  - [ ] `T03-10` Build genesis progress + feed/overview shell from real API

## Epic `EP-S03-03` – Replay & Snapshot Confidence

- [ ] Epic complete

### Issue `ADW-S03-BE-01` – Deterministic checks

- [ ] Issue complete
- Depends on: `T03-05`, `T03-07`
- Subtasks:
  - [ ] `T03-09` Add snapshot/replay tests cho genesis path

### Issue `ADW-S03-DO-01` – Smoke/demo profile

- [ ] Issue complete
- Depends on: `T03-09`
- Subtasks:
  - [ ] `T03-11` Add mock/live profiles and genesis smoke path

## Verification Checklist

- [ ] Genesis produces non-empty world in scope
- [ ] Contract tests pass
- [ ] Snapshot replay stable
