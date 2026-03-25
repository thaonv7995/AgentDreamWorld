# Sprint 19 – Task Breakdown

## Breakdown Goal

Tạo shareable world package và gallery layer với trust boundaries, provenance và compatibility là phần core chứ không phải extra.

## Work Packages

- `WP1` Package format and validation
- `WP2` Gallery APIs and UX
- `WP3` Trust and moderation baseline

## Atomic Tasks

| ID | Parent | Stream | Task | Depends On | Output |
| --- | --- | --- | --- | --- | --- |
| T19-01 | ADW-S19-BA-01 | BA | Chốt world package schema, gallery item schema và import validation rules | None | package/gallery contract |
| T19-02 | ADW-S19-BE-01 | Backend | Build stable package export for seed, history và metadata | T18-05,T19-01 | package export |
| T19-03 | ADW-S19-BE-01 | Backend | Implement package import validation và compatibility checks trước activation | T19-01,T19-02 | import validator |
| T19-04 | ADW-S19-BE-01 | Backend | Expose gallery APIs với provenance, compatibility và moderation metadata | T19-02,T19-03 | gallery API |
| T19-05 | ADW-S19-FE-01 | Frontend | Build package import/export flows | T19-02,T19-03 | package flow UI |
| T19-06 | ADW-S19-FE-01 | Frontend | Build gallery browse/filter surfaces | T19-04 | gallery browse UI |
| T19-07 | ADW-S19-FE-01 | Frontend | Add provenance/version badges và import validation states | T19-03,T19-06 | trust-state UX |
| T19-08 | ADW-S19-DO-01 | DevOps | Run export -> import round-trip smoke tests và compatibility matrix | T19-07 | round-trip report |
| T19-09 | ADW-S19-DO-01 | DevOps | Write moderation/runbook basics và trust-boundary review note | T19-04,T19-08 | moderation baseline |

## Suggested Sequence

1. `T19-01`
2. `T19-02 -> T19-03 -> T19-04`
3. `T19-05 -> T19-06 -> T19-07`
4. `T19-08 -> T19-09`

## Cut Line

- Must-have: `T19-01..T19-08`
- Can defer: `T19-09` moderation depth

## Verification Artifacts

- Export -> import round trip thành công
- Gallery items đủ understandable và trustworthy để browse
- Shared worlds hữu ích ngay cả khi chưa có live collaboration
