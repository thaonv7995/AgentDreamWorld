# Sprint 18 – Task Breakdown

## Breakdown Goal

Biến exports thành creator publishing pipeline có bundle, manifest và provenance/version rõ ràng.

## Work Packages

- `WP1` Artifact assembly
- `WP2` Creator bundle UX
- `WP3` Artifact retention and recovery

## Atomic Tasks

| ID | Parent | Stream | Task | Depends On | Output |
| --- | --- | --- | --- | --- | --- |
| T18-01 | ADW-S18-BA-01 | BA | Chốt creator bundle structure, highlight manifest schema và provenance/version fields | None | creator bundle contract |
| T18-02 | ADW-S18-BE-01 | Backend | Implement myths export assembly | T10-05,T18-01 | myths export |
| T18-03 | ADW-S18-BE-01 | Backend | Implement arc export packs | T15-04,T18-01 | arc export |
| T18-04 | ADW-S18-BE-01 | Backend | Implement highlight manifest generator | T18-01,T18-03 | highlight manifest |
| T18-05 | ADW-S18-BE-01 | Backend | Assemble unified creator bundle từ canonical world, branch và artifact metadata | T16-04,T17-06,T18-02,T18-03,T18-04 | creator bundle assembler |
| T18-06 | ADW-S18-BE-01 | Backend | Add optional remote artifact path sau cùng bundle contract | T18-05 | optional remote storage path |
| T18-07 | ADW-S18-FE-01 | Frontend | Build creator bundle export entry point | T18-05 | export entry UI |
| T18-08 | ADW-S18-FE-01 | Frontend | Build bundle contents preview, download states và cross-links từ myths/arcs/highlights | T18-05,T18-07 | bundle preview UI |
| T18-09 | ADW-S18-DO-01 | DevOps | Define artifact retention policy, run bundle smoke suite và write recovery notes | T18-06,T18-08 | artifact ops baseline |

## Suggested Sequence

1. `T18-01`
2. `T18-02 -> T18-03 -> T18-04`
3. `T18-05 -> T18-06`
4. `T18-07 -> T18-08`
5. `T18-09`

## Cut Line

- Must-have: `T18-01..T18-08`
- Can defer: `T18-09` remote-path support depth

## Verification Artifacts

- Creator bundle usable không cần stitching tay
- Myths/arcs/highlights link ngược về source world/branch
- Optional remote path không đổi semantics của bundle
