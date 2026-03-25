# Sprint 09 – Issue-Ready Board

## Suggested Order

`EP-S09-01` -> `EP-S09-02` -> `EP-S09-03`

## Epic `EP-S09-01` – Spatial Projections

- [ ] Epic complete

### Issue `ADW-S09-BA-01` – Map/civ contract

- [ ] Issue complete
- Depends on: `ADW-S08-BA-01`
- Subtasks:
  - [ ] `T09-01` Chốt map projection shape, civ payload và ownership semantics

### Issue `ADW-S09-BE-01` – Geography projections

- [ ] Issue complete
- Depends on: `T08-05`, `T09-01`
- Subtasks:
  - [ ] `T09-02` Build region/world map projection từ world model hiện có
  - [ ] `T09-03` Build territory ownership projection
  - [ ] `T09-04` Build civilization detail read model với history và settlement summaries
  - [ ] `T09-05` Add settlement distribution summary cho map/civ surfaces

## Epic `EP-S09-02` – Map & Civilization Surfaces

- [ ] Epic complete

### Issue `ADW-S09-FE-01` – Map beta và civ viewer

- [ ] Issue complete
- Depends on: `T09-02`, `T09-04`
- Subtasks:
  - [ ] `T09-06` Render map beta từ projection thật
  - [ ] `T09-07` Build Civilization Viewer và navigation từ feed/timeline sang civ detail
  - [ ] `T09-08` Handle sparse-world fallback states và empty geography gracefully

## Epic `EP-S09-03` – Visual Quality & Performance

- [ ] Epic complete

### Issue `ADW-S09-DO-01` – Visual/perf baseline

- [ ] Issue complete
- Depends on: `T09-05`, `T09-08`
- Subtasks:
  - [ ] `T09-09` Set perf budget cho map rendering, visual QA snapshots và spatially diverse seeds

## Verification Checklist

- [ ] Map render được nhiều world không cần tweak tay
- [ ] Civilization Viewer khớp backend state
- [ ] Feed -> civ -> map navigation chạy thông
