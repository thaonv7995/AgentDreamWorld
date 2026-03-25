# Sprint 12 – Issue-Ready Board

## Suggested Order

`EP-S12-01` -> `EP-S12-02` -> `EP-S12-03`

## Epic `EP-S12-01` – World Metadata & Indirection

- [ ] Epic complete

### Issue `ADW-S12-BA-01` – Multi-world contract baseline

- [ ] Issue complete
- Depends on: `ADW-S11-BA-01`
- Subtasks:
  - [ ] `T12-01` Chốt world metadata schema, current-world semantics và snapshot provenance baseline

### Issue `ADW-S12-BE-01` – Registry và metadata separation

- [ ] Issue complete
- Depends on: `T12-01`
- Subtasks:
  - [ ] `T12-02` Add world registry và current-world indirection trong core flows
  - [ ] `T12-03` Separate world metadata khỏi world state ở nơi cần thiết
  - [ ] `T12-05` Remove hard-coded single-world assumptions khỏi generation, feed, export và config paths

### Issue `ADW-S12-FE-01` – Selector shell

- [ ] Issue complete
- Depends on: `T12-02`
- Subtasks:
  - [ ] `T12-06` Build minimal current-world selector/list shell

## Epic `EP-S12-02` – Snapshot/Fork Hooks

- [ ] Epic complete

### Issue `ADW-S12-BE-01` – Fork foundation

- [ ] Issue complete
- Depends on: `T12-01`, `T12-03`
- Subtasks:
  - [ ] `T12-04` Add snapshot/fork hooks baseline chưa gắn final UX semantics

## Epic `EP-S12-03` – Recovery & Multi-world Ops

- [ ] Epic complete

### Issue `ADW-S12-DO-01` – Recovery flows và monitoring

- [ ] Issue complete
- Depends on: `T12-03`, `T12-04`
- Subtasks:
  - [ ] `T12-07` Implement backup/restore flows cho multiple worlds
  - [ ] `T12-08` Add world growth monitoring labels và run recovery drill cho snapshot metadata path

## Verification Checklist

- [ ] Current-world UX cũ vẫn hoạt động
- [ ] Multi-world metadata survive restart/reload
- [ ] Core flows không còn assumption kiểu single world forever
