# Sprint 00 – Task Breakdown

## Breakdown Goal

Biến repo từ `docs-only` thành runnable skeleton có walking skeleton end-to-end.

## Work Packages

- `WP1` Repo skeleton
- `WP2` Local dev rail
- `WP3` Walking skeleton flow

## Atomic Tasks

| ID | Parent | Stream | Task | Depends On | Output |
| --- | --- | --- | --- | --- | --- |
| T00-01 | ADW-S00-BE-01 | Backend | Tạo Rust workspace và binary `ai-dreams-server` | None | workspace chạy được |
| T00-02 | ADW-S00-BE-01 | Backend | Thêm health endpoint và stub tick/events endpoints | T00-01 | stub API |
| T00-03 | ADW-S00-FE-01 | Frontend | Tạo React/Vite shell | None | frontend shell |
| T00-04 | ADW-S00-DO-01 | DevOps | Tạo `.env.example`, `dev.sh`, command matrix | T00-01,T00-03 | local dev rail |
| T00-05 | ADW-S00-BE-01 | Backend | Thêm process modes CLI baseline | T00-01 | mode contract |
| T00-06 | ADW-S00-FE-01 | Frontend | Call stub API thật từ shell | T00-02,T00-03 | UI render dữ liệu thật |
| T00-07 | ADW-S00-DO-01 | DevOps | Thiết lập CI tối thiểu cho build/lint/smoke | T00-02,T00-03 | CI baseline |
| T00-08 | ADW-S00-BA-01 | BA | Chốt acceptance criteria và onboarding path | T00-04 | sign-off checklist |

## Suggested Sequence

1. `T00-01` -> `T00-02` và `T00-03`
2. `T00-04` + `T00-05`
3. `T00-06`
4. `T00-07` + `T00-08`

## Cut Line

- Must-have: `T00-01..T00-06`
- Can defer if needed: `T00-07`

## Verification Artifacts

- `cargo run --bin ai-dreams-server`
- `npm run dev`
- POST stub tick -> GET events -> UI render
