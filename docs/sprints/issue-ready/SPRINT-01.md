# Sprint 01 – Issue-Ready Board

## Suggested Order

`EP-S01-01` -> `EP-S01-02` -> `EP-S01-03`

## Epic `EP-S01-01` – Canon Schema

- [ ] Epic complete

### Issue `ADW-S01-BA-01` – Glossary entity và world contract

- [ ] Issue complete
- Depends on: `ADW-S00-BA-01`
- Subtasks:
  - [ ] `T01-01` Chốt glossary entity V1 và response contract `GET /worlds/current`

### Issue `ADW-S01-BE-01` – Schema SQLite V1 và init flow

- [ ] Issue complete
- Depends on: `T01-01`
- Subtasks:
  - [ ] `T01-02` Tạo migrations cho core tables và `eras`
  - [ ] `T01-03` Implement DB init + schema version tracking
  - [ ] `T01-04` Implement database-per-world path resolution

## Epic `EP-S01-02` – Repository & Read Model

- [ ] Epic complete

### Issue `ADW-S01-BE-01` – Repository/read path

- [ ] Issue complete
- Depends on: `T01-03`
- Subtasks:
  - [ ] `T01-05` Implement repositories cho world summary + events read path

### Issue `ADW-S01-FE-01` – Overview shell

- [ ] Issue complete
- Depends on: `T01-01`, `T01-06`
- Subtasks:
  - [ ] `T01-07` Tạo world summary types và overview shell

## Epic `EP-S01-03` – Seed & Smoke Path

- [ ] Epic complete

### Issue `ADW-S01-BE-01` – Seed world baseline

- [ ] Issue complete
- Depends on: `T01-05`
- Subtasks:
  - [ ] `T01-06` Tạo seed world không dùng LLM

### Issue `ADW-S01-DO-01` – DB smoke path

- [ ] Issue complete
- Depends on: `T01-06`
- Subtasks:
  - [ ] `T01-08` Smoke test DB init/restart/seed path

## Verification Checklist

- [ ] Seed world readable after restart
- [ ] `GET /worlds/current` trả về dữ liệu thật
