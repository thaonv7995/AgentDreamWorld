# Sprint 16 – Issue-Ready Board

## Suggested Order

`EP-S16-01` -> `EP-S16-02` -> `EP-S16-03`

## Epic `EP-S16-01` – Fork & Branch Runtime

- [ ] Epic complete

### Issue `ADW-S16-BA-01` – Branch/snapshot contract

- [ ] Issue complete
- Depends on: `ADW-S15-BA-01`
- Subtasks:
  - [ ] `T16-01` Chốt branch provenance schema, compare projection shape và snapshot metadata

### Issue `ADW-S16-BE-01` – Fork runtime

- [ ] Issue complete
- Depends on: `T12-04`, `T16-01`
- Subtasks:
  - [ ] `T16-02` Implement world forking tại year, era hoặc event checkpoint
  - [ ] `T16-03` Isolate mainline và branch trong runtime scheduling và state storage

## Epic `EP-S16-02` – Divergence Compare

- [ ] Epic complete

### Issue `ADW-S16-BE-01` – Compare payloads

- [ ] Issue complete
- Depends on: `T16-02`, `T16-03`
- Subtasks:
  - [ ] `T16-04` Build compare projections tóm tắt divergence thay vì raw diff thuần

### Issue `ADW-S16-FE-01` – Branch compare UX

- [ ] Issue complete
- Depends on: `T16-02`, `T16-04`
- Subtasks:
  - [ ] `T16-05` Build fork flow từ timeline/checkpoint surfaces
  - [ ] `T16-06` Build branch navigation và compare views

## Epic `EP-S16-03` – Snapshot Portability & Ops

- [ ] Epic complete

### Issue `ADW-S16-FE-01` – Snapshot sharing UI

- [ ] Issue complete
- Depends on: `T16-01`, `T16-06`
- Subtasks:
  - [ ] `T16-07` Build snapshot share/export states

### Issue `ADW-S16-DO-01` – Branch/snapshot operations

- [ ] Issue complete
- Depends on: `T16-03`, `T16-07`
- Subtasks:
  - [ ] `T16-08` Define retention/cleanup policy cho branches và snapshots
  - [ ] `T16-09` Run restore drills và storage growth monitoring cho branch path

## Verification Checklist

- [ ] Branch diverge và tiếp tục independently
- [ ] Compare view giải thích được civilizations/regions/events changed
- [ ] Snapshot sharing portable và auditable
