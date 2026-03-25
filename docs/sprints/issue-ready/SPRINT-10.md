# Sprint 10 – Issue-Ready Board

## Suggested Order

`EP-S10-01` -> `EP-S10-02` -> `EP-S10-03`

## Epic `EP-S10-01` – Entity Linking & Graph Projection

- [ ] Epic complete

### Issue `ADW-S10-BA-01` – Graph/browser contract

- [ ] Issue complete
- Depends on: `ADW-S09-BA-01`
- Subtasks:
  - [ ] `T10-01` Chốt graph node/edge taxonomy, mythology browser categories và linked export semantics

### Issue `ADW-S10-BE-01` – Entity linking và graph projection

- [ ] Issue complete
- Depends on: `T09-04`, `T09-05`, `T10-01`
- Subtasks:
  - [ ] `T10-02` Build entity linking pipeline giữa civ, myth, event, region và settlement
  - [ ] `T10-03` Build graph-friendly node/edge projections có explainable source links
  - [ ] `T10-04` Implement browser/query APIs với safe bounds cho V2 world size

## Epic `EP-S10-02` – Lore Browser & Graph UI

- [ ] Epic complete

### Issue `ADW-S10-FE-01` – Mythology Browser và graph explorer

- [ ] Issue complete
- Depends on: `T10-03`, `T10-04`
- Subtasks:
  - [ ] `T10-06` Build Mythology Browser views và category navigation
  - [ ] `T10-07` Build Knowledge Graph beta với safe defaults và filters
  - [ ] `T10-08` Add cross-navigation giữa graph, timeline, map và civ detail

## Epic `EP-S10-03` – Linked Export & Performance Safety

- [ ] Epic complete

### Issue `ADW-S10-BE-01` – Linked export path

- [ ] Issue complete
- Depends on: `T10-03`, `T10-04`
- Subtasks:
  - [ ] `T10-05` Extend export pipeline để preserve linked relationships

### Issue `ADW-S10-DO-01` – Graph perf baseline

- [ ] Issue complete
- Depends on: `T10-05`, `T10-08`
- Subtasks:
  - [ ] `T10-09` Measure graph query latency/render perf và prepare dense-link sample worlds

## Verification Checklist

- [ ] Graph usable ở target V2 world size
- [ ] Mythology Browser link tới entities/events thật
- [ ] Linked export giữ được quan hệ cốt lõi
