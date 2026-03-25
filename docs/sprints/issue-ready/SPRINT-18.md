# Sprint 18 – Issue-Ready Board

## Suggested Order

`EP-S18-01` -> `EP-S18-02` -> `EP-S18-03`

## Epic `EP-S18-01` – Artifact Assembly

- [ ] Epic complete

### Issue `ADW-S18-BA-01` – Creator bundle contract

- [ ] Issue complete
- Depends on: `ADW-S17-BA-01`
- Subtasks:
  - [ ] `T18-01` Chốt creator bundle structure, highlight manifest schema và provenance/version fields

### Issue `ADW-S18-BE-01` – Bundle assembly backend

- [ ] Issue complete
- Depends on: `T10-05`, `T15-04`, `T18-01`
- Subtasks:
  - [ ] `T18-02` Implement myths export assembly
  - [ ] `T18-03` Implement arc export packs
  - [ ] `T18-04` Implement highlight manifest generator
  - [ ] `T18-05` Assemble unified creator bundle từ canonical world, branch và artifact metadata
  - [ ] `T18-06` Add optional remote artifact path sau cùng bundle contract

## Epic `EP-S18-02` – Creator Bundle UX

- [ ] Epic complete

### Issue `ADW-S18-FE-01` – Export and preview UI

- [ ] Issue complete
- Depends on: `T18-05`
- Subtasks:
  - [ ] `T18-07` Build creator bundle export entry point
  - [ ] `T18-08` Build bundle contents preview, download states và cross-links từ myths/arcs/highlights

## Epic `EP-S18-03` – Artifact Retention & Recovery

- [ ] Epic complete

### Issue `ADW-S18-DO-01` – Artifact operations

- [ ] Issue complete
- Depends on: `T18-06`, `T18-08`
- Subtasks:
  - [ ] `T18-09` Define artifact retention policy, run bundle smoke suite và write recovery notes

## Verification Checklist

- [ ] Creator bundle usable không cần stitching tay
- [ ] Myths/arcs/highlights link ngược về source world/branch
- [ ] Optional remote path không đổi semantics của bundle
