# Sprint 15 – Issue-Ready Board

## Suggested Order

`EP-S15-01` -> `EP-S15-02` -> `EP-S15-03`

## Epic `EP-S15-01` – Advanced God Mode

- [ ] Epic complete

### Issue `ADW-S15-BA-01` – Intervention/arc contract

- [ ] Issue complete
- Depends on: `ADW-S14-BA-01`
- Subtasks:
  - [ ] `T15-01` Chốt intervention request schema, arc card schema và explainability fields

### Issue `ADW-S15-BE-01` – Governed intervention path

- [ ] Issue complete
- Depends on: `T14-03`, `T15-01`
- Subtasks:
  - [ ] `T15-02` Model advanced interventions thành proposals hoặc controlled commands

### Issue `ADW-S15-FE-01` – Creator control UI

- [ ] Issue complete
- Depends on: `T15-03`
- Subtasks:
  - [ ] `T15-05` Build Advanced God Mode forms với safe defaults

## Epic `EP-S15-02` – Intervention Guardrails

- [ ] Epic complete

### Issue `ADW-S15-BE-01` – Intervention guardrails

- [ ] Issue complete
- Depends on: `T15-02`
- Subtasks:
  - [ ] `T15-03` Add guardrails, validation và canonicalization cho intervention flow

### Issue `ADW-S15-DO-01` – Intervention regression

- [ ] Issue complete
- Depends on: `T15-03`, `T15-04`
- Subtasks:
  - [ ] `T15-08` Build coherence regression set cho intervention-heavy runs

## Epic `EP-S15-03` – Story Arc Extraction & UX

- [ ] Epic complete

### Issue `ADW-S15-BE-01` – Arc extraction pipeline

- [ ] Issue complete
- Depends on: `T10-03`, `T15-01`
- Subtasks:
  - [ ] `T15-04` Build story arc extraction/scoring từ canonical events, summaries và myth layers

### Issue `ADW-S15-FE-01` – Arc surfaces

- [ ] Issue complete
- Depends on: `T15-04`
- Subtasks:
  - [ ] `T15-06` Build arc cards/panels linked vào timeline và browser surfaces
  - [ ] `T15-07` Tách viewer tooling và creator tooling rõ ràng trong UX

### Issue `ADW-S15-DO-01` – Creator demo baseline

- [ ] Issue complete
- Depends on: `T15-08`
- Subtasks:
  - [ ] `T15-09` Review cost/latency và chọn demo worlds có arc emergence mạnh

## Verification Checklist

- [ ] Interventions để lại consequence traceable
- [ ] Guardrails chặn destructive hoặc invalid changes
- [ ] Arc highlighter cho ra story slices usable
