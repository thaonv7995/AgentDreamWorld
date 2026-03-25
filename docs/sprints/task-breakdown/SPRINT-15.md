# Sprint 15 – Task Breakdown

## Breakdown Goal

Thêm creator-grade intervention và story curation nhưng mọi can thiệp vẫn phải đi qua governed simulation path.

## Work Packages

- `WP1` Advanced God Mode
- `WP2` Intervention guardrails
- `WP3` Story arc extraction and UX

## Atomic Tasks

| ID | Parent | Stream | Task | Depends On | Output |
| --- | --- | --- | --- | --- | --- |
| T15-01 | ADW-S15-BA-01 | BA | Chốt intervention request schema, arc card schema và explainability fields | None | intervention/arc contract |
| T15-02 | ADW-S15-BE-01 | Backend | Model advanced interventions thành proposals hoặc controlled commands | T14-03,T15-01 | governed intervention path |
| T15-03 | ADW-S15-BE-01 | Backend | Add guardrails, validation và canonicalization cho intervention flow | T15-02 | intervention guardrails |
| T15-04 | ADW-S15-BE-01 | Backend | Build story arc extraction/scoring từ canonical events, summaries và myth layers | T10-03,T15-01 | arc extraction pipeline |
| T15-05 | ADW-S15-FE-01 | Frontend | Build Advanced God Mode forms với safe defaults | T15-03 | creator control UI |
| T15-06 | ADW-S15-FE-01 | Frontend | Build arc cards/panels linked vào timeline và browser surfaces | T15-04 | story arc UI |
| T15-07 | ADW-S15-FE-01 | Frontend | Tách viewer tooling và creator tooling rõ ràng trong UX | T15-05,T15-06 | role-separated UX |
| T15-08 | ADW-S15-DO-01 | DevOps | Build coherence regression set cho intervention-heavy runs | T15-03,T15-04 | intervention regression suite |
| T15-09 | ADW-S15-DO-01 | DevOps | Review cost/latency và chọn demo worlds có arc emergence mạnh | T15-08 | creator demo baseline |

## Suggested Sequence

1. `T15-01`
2. `T15-02 -> T15-03`
3. `T15-04`
4. `T15-05 -> T15-06 -> T15-07`
5. `T15-08 -> T15-09`

## Cut Line

- Must-have: `T15-01..T15-08`
- Can defer: `T15-09` demo curation depth

## Verification Artifacts

- Interventions để lại consequence traceable
- Guardrails chặn destructive hoặc invalid changes
- Arc highlighter cho ra story slices usable
