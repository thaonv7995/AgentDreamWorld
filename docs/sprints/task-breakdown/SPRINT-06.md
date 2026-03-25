# Sprint 06 – Task Breakdown

## Breakdown Goal

Đạt Gate D với MVP path world generation -> observation -> export -> single-binary delivery.

## Work Packages

- `WP1` Export pipeline
- `WP2` Single-binary delivery
- `WP3` MVP hardening and sign-off

## Atomic Tasks

| ID | Parent | Stream | Task | Depends On | Output |
| --- | --- | --- | --- | --- | --- |
| T06-01 | ADW-S06-BA-01 | BA | Chốt wiki/annals output contract và MVP DoD sign-off pack | None | export + DoD contract |
| T06-02 | ADW-S06-BE-01 | Backend | Implement wiki export assembly | T05-02,T06-01 | wiki export |
| T06-03 | ADW-S06-BE-01 | Backend | Implement annals export assembly | T05-02,T06-01 | annals export |
| T06-04 | ADW-S06-BE-01 | Backend | Implement backend serve static frontend in single-binary mode | T00-03,T06-02 | single-binary backend |
| T06-05 | ADW-S06-FE-01 | Frontend | Implement export actions and status states | T06-02,T06-03 | export UI |
| T06-06 | ADW-S06-FE-01 | Frontend | Polish MVP path and remove mock-only UX leftovers | T05-05,T05-06 | MVP UI polish |
| T06-07 | ADW-S06-BE-01 | Backend | Fix blocker bugs on generation/observer/export path | T06-02,T06-03,T06-04 | hardened MVP path |
| T06-08 | ADW-S06-DO-01 | DevOps | Build release pipeline and smoke single-binary/export flow | T06-04,T06-05 | release artifact |
| T06-09 | ADW-S06-DO-01 | DevOps | Prepare release notes, install notes, Gate D demo path | T06-08,T06-01 | release/sign-off pack |

## Suggested Sequence

1. `T06-01`
2. `T06-02` + `T06-03`
3. `T06-04`
4. `T06-05` + `T06-06`
5. `T06-07`
6. `T06-08 -> T06-09`

## Cut Line

- Must-have: `T06-01..T06-08`
- Can defer: `T06-09` polish depth

## Verification Artifacts

- Single-binary artifact runs locally
- Wiki and annals exports readable
- Gate D demo path complete end-to-end
