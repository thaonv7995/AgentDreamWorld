# Sprint 00 – Issue-Ready Board

## Suggested Order

`EP-S00-01` -> `EP-S00-02` -> `EP-S00-03`

## Epic `EP-S00-01` – Repo Skeleton

- [ ] Epic complete

### Issue `ADW-S00-BE-01` – Rust workspace và stub backend

- [ ] Issue complete
- Depends on: `None`
- Subtasks:
  - [ ] `T00-01` Tạo Rust workspace và binary `ai-dreams-server`
  - [ ] `T00-02` Thêm health endpoint và stub tick/events endpoints
  - [ ] `T00-05` Thêm process modes CLI baseline

## Epic `EP-S00-02` – Local Dev Rail

- [ ] Epic complete

### Issue `ADW-S00-FE-01` – React/Vite app shell

- [ ] Issue complete
- Depends on: `None`
- Subtasks:
  - [ ] `T00-03` Tạo React/Vite shell
  - [ ] `T00-06` Call stub API thật từ shell

### Issue `ADW-S00-DO-01` – Dev rail và CI baseline

- [ ] Issue complete
- Depends on: `T00-01`, `T00-03`
- Subtasks:
  - [ ] `T00-04` Tạo `.env.example`, `dev.sh`, command matrix
  - [ ] `T00-07` Thiết lập CI tối thiểu cho build/lint/smoke

## Epic `EP-S00-03` – Walking Skeleton Sign-off

- [ ] Epic complete

### Issue `ADW-S00-BA-01` – Acceptance criteria và onboarding path

- [ ] Issue complete
- Depends on: `T00-04`
- Subtasks:
  - [ ] `T00-08` Chốt acceptance criteria và onboarding path

## Verification Checklist

- [ ] `cargo run --bin ai-dreams-server`
- [ ] `npm run dev`
- [ ] POST stub tick -> GET events -> UI render
