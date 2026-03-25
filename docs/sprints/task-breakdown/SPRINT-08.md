# Sprint 08 – Task Breakdown

## Breakdown Goal

Thêm macro causality cho world simulation mà không làm coherence collapse.

## Work Packages

- `WP1` Macro agents
- `WP2` Propagation and tuning
- `WP3` Observer impact surfaces

## Atomic Tasks

| ID | Parent | Stream | Task | Depends On | Output |
| --- | --- | --- | --- | --- | --- |
| T08-01 | ADW-S08-BA-01 | BA | Chốt macro event taxonomy, propagation semantics và coherence thresholds | None | macro rules contract |
| T08-02 | ADW-S08-BE-01 | Backend | Implement Ecology agent | T07-06,T08-01 | ecology path |
| T08-03 | ADW-S08-BE-01 | Backend | Implement Economy agent | T07-06,T08-01 | economy path |
| T08-04 | ADW-S08-BE-01 | Backend | Implement Chaos agent | T07-06,T08-01 | chaos path |
| T08-05 | ADW-S08-BE-01 | Backend | Implement scarcity/conflict/collapse propagation rules | T08-02,T08-03,T08-04 | propagation engine |
| T08-06 | ADW-S08-BE-01 | Backend | Expand Guardian/Historian scoring hooks để quan sát reject rate và chaos rate | T08-05 | tuning metrics hooks |
| T08-07 | ADW-S08-FE-01 | Frontend | Extend feed/timeline labels cho macro event categories | T08-05 | macro event labels |
| T08-08 | ADW-S08-FE-01 | Frontend | Add filters và impact badges tối thiểu cho macro events | T08-07 | macro filters UI |
| T08-09 | ADW-S08-DO-01 | DevOps | Run long-run simulation tests và tune instability thresholds | T08-06,T08-08 | tuning dataset |
| T08-10 | ADW-S08-DO-01 | DevOps | Compare runs trước/sau tuning và chốt balance note | T08-09 | balance report |

## Suggested Sequence

1. `T08-01`
2. `T08-02..T08-04`
3. `T08-05 -> T08-06`
4. `T08-07 -> T08-08`
5. `T08-09 -> T08-10`

## Cut Line

- Must-have: `T08-01..T08-09`
- Can defer: `T08-10` comparative reporting depth

## Verification Artifacts

- Variety event tăng mà invalid spike vẫn trong ngưỡng
- Trade/ecology/scarcity tạo chain hậu quả giải thích được
- Observer surfaces vẫn readable sau expansion
