# Sprint 07 – Issue-Ready Board

## Suggested Order

`EP-S07-01` -> `EP-S07-02` -> `EP-S07-03`

## Epic `EP-S07-01` – Culture/Myth Generation

- [ ] Epic complete

### Issue `ADW-S07-BA-01` – Lore taxonomy và era summary contract

- [ ] Issue complete
- Depends on: `ADW-S06-BA-01`
- Subtasks:
  - [ ] `T07-01` Chốt era summary schema, myth/culture taxonomy và acceptance criteria

### Issue `ADW-S07-BE-01` – Culture/Myth generation path

- [ ] Issue complete
- Depends on: `T03-05`, `T07-01`
- Subtasks:
  - [ ] `T07-02` Implement Culture agent qua runtime abstraction hiện có
  - [ ] `T07-03` Implement Myth agent qua runtime abstraction hiện có
  - [ ] `T07-04` Persist myth/culture outputs thành tags hoặc soft refs có thể query được

## Epic `EP-S07-02` – Era Summary Compression

- [ ] Epic complete

### Issue `ADW-S07-BE-01` – Summary artifacts và context selection

- [ ] Issue complete
- Depends on: `T07-01`, `T07-04`
- Subtasks:
  - [ ] `T07-05` Implement era summary generator và compressed artifact persistence
  - [ ] `T07-06` Implement context selection rules ưu tiên era summaries thay cho raw history

## Epic `EP-S07-03` – Projection/UI & Context Quality

- [ ] Epic complete

### Issue `ADW-S07-FE-01` – Myth/culture surfaces

- [ ] Issue complete
- Depends on: `T07-04`, `T07-06`
- Subtasks:
  - [ ] `T07-07` Show culture/myth tags trên feed và overview surfaces
  - [ ] `T07-08` Add era summary panel và navigation states tối thiểu

### Issue `ADW-S07-DO-01` – Prompt versioning và era soak

- [ ] Issue complete
- Depends on: `T07-02`, `T07-03`, `T07-08`
- Subtasks:
  - [ ] `T07-09` Version prompt/rule sets cho culture/myth path
  - [ ] `T07-10` Soak era transition path và đo token/context savings

## Verification Checklist

- [ ] Era summaries đủ để replace phần lớn raw-history context
- [ ] Feed/world overview đã có myth/culture surface đọc được
- [ ] Era transition không gây context regression lớn
