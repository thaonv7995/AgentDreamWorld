# Sprint 19 – Issue-Ready Board

## Suggested Order

`EP-S19-01` -> `EP-S19-02` -> `EP-S19-03`

## Epic `EP-S19-01` – Package Format & Validation

- [ ] Epic complete

### Issue `ADW-S19-BA-01` – Package/gallery contract

- [ ] Issue complete
- Depends on: `ADW-S18-BA-01`
- Subtasks:
  - [ ] `T19-01` Chốt world package schema, gallery item schema và import validation rules

### Issue `ADW-S19-BE-01` – Package export/import validation

- [ ] Issue complete
- Depends on: `T18-05`, `T19-01`
- Subtasks:
  - [ ] `T19-02` Build stable package export for seed, history và metadata
  - [ ] `T19-03` Implement package import validation và compatibility checks trước activation

## Epic `EP-S19-02` – Gallery APIs & UX

- [ ] Epic complete

### Issue `ADW-S19-BE-01` – Gallery API

- [ ] Issue complete
- Depends on: `T19-02`, `T19-03`
- Subtasks:
  - [ ] `T19-04` Expose gallery APIs với provenance, compatibility và moderation metadata

### Issue `ADW-S19-FE-01` – Community gallery UI

- [ ] Issue complete
- Depends on: `T19-02`, `T19-03`, `T19-04`
- Subtasks:
  - [ ] `T19-05` Build package import/export flows
  - [ ] `T19-06` Build gallery browse/filter surfaces
  - [ ] `T19-07` Add provenance/version badges và import validation states

## Epic `EP-S19-03` – Trust & Moderation Baseline

- [ ] Epic complete

### Issue `ADW-S19-DO-01` – Package trust operations

- [ ] Issue complete
- Depends on: `T19-04`, `T19-07`
- Subtasks:
  - [ ] `T19-08` Run export -> import round-trip smoke tests và compatibility matrix
  - [ ] `T19-09` Write moderation/runbook basics và trust-boundary review note

## Verification Checklist

- [ ] Export -> import round trip thành công
- [ ] Gallery items đủ understandable và trustworthy để browse
- [ ] Shared worlds hữu ích ngay cả khi chưa có live collaboration
