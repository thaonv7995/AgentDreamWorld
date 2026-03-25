# Sprint 06 – Issue-Ready Board

## Suggested Order

`EP-S06-01` -> `EP-S06-02` -> `EP-S06-03`

## Epic `EP-S06-01` – Export Pipeline

- [ ] Epic complete

### Issue `ADW-S06-BA-01` – Export contract và MVP DoD

- [ ] Issue complete
- Depends on: `ADW-S05-BA-01`
- Subtasks:
  - [ ] `T06-01` Chốt wiki/annals output contract và MVP DoD sign-off pack

### Issue `ADW-S06-BE-01` – Wiki/annals export

- [ ] Issue complete
- Depends on: `T05-02`, `T06-01`
- Subtasks:
  - [ ] `T06-02` Implement wiki export assembly
  - [ ] `T06-03` Implement annals export assembly

### Issue `ADW-S06-FE-01` – Export UI

- [ ] Issue complete
- Depends on: `T06-02`, `T06-03`
- Subtasks:
  - [ ] `T06-05` Implement export actions and status states

## Epic `EP-S06-02` – Single-Binary Delivery

- [ ] Epic complete

### Issue `ADW-S06-BE-01` – Serve frontend from backend

- [ ] Issue complete
- Depends on: `T00-03`, `T06-02`
- Subtasks:
  - [ ] `T06-04` Implement backend serve static frontend in single-binary mode

### Issue `ADW-S06-DO-01` – Release artifact

- [ ] Issue complete
- Depends on: `T06-04`, `T06-05`
- Subtasks:
  - [ ] `T06-08` Build release pipeline and smoke single-binary/export flow

## Epic `EP-S06-03` – MVP Hardening & Sign-off

- [ ] Epic complete

### Issue `ADW-S06-FE-01` – MVP polish

- [ ] Issue complete
- Depends on: `T05-05`, `T05-06`
- Subtasks:
  - [ ] `T06-06` Polish MVP path and remove mock-only UX leftovers

### Issue `ADW-S06-BE-01` – Blocker fixes

- [ ] Issue complete
- Depends on: `T06-02`, `T06-03`, `T06-04`
- Subtasks:
  - [ ] `T06-07` Fix blocker bugs on generation/observer/export path

### Issue `ADW-S06-DO-01` – Release/sign-off pack

- [ ] Issue complete
- Depends on: `T06-08`, `T06-01`
- Subtasks:
  - [ ] `T06-09` Prepare release notes, install notes, Gate D demo path

## Verification Checklist

- [ ] Single-binary artifact runs locally
- [ ] Wiki and annals exports readable
- [ ] Gate D demo path complete end-to-end
