# Sprint 08 – Issue-Ready Board

## Suggested Order

`EP-S08-01` -> `EP-S08-02` -> `EP-S08-03`

## Epic `EP-S08-01` – Macro Agents

- [ ] Epic complete

### Issue `ADW-S08-BA-01` – Macro rules contract

- [ ] Issue complete
- Depends on: `ADW-S07-BA-01`
- Subtasks:
  - [ ] `T08-01` Chốt macro event taxonomy, propagation semantics và coherence thresholds

### Issue `ADW-S08-BE-01` – Ecology/Economy/Chaos agents

- [ ] Issue complete
- Depends on: `T07-06`, `T08-01`
- Subtasks:
  - [ ] `T08-02` Implement Ecology agent
  - [ ] `T08-03` Implement Economy agent
  - [ ] `T08-04` Implement Chaos agent

## Epic `EP-S08-02` – Propagation & Tuning

- [ ] Epic complete

### Issue `ADW-S08-BE-01` – Propagation engine

- [ ] Issue complete
- Depends on: `T08-02`, `T08-03`, `T08-04`
- Subtasks:
  - [ ] `T08-05` Implement scarcity/conflict/collapse propagation rules
  - [ ] `T08-06` Expand Guardian/Historian scoring hooks để quan sát reject rate và chaos rate

### Issue `ADW-S08-DO-01` – Long-run tuning

- [ ] Issue complete
- Depends on: `T08-06`, `T08-08`
- Subtasks:
  - [ ] `T08-09` Run long-run simulation tests và tune instability thresholds
  - [ ] `T08-10` Compare runs trước/sau tuning và chốt balance note

## Epic `EP-S08-03` – Observer Impact Surfaces

- [ ] Epic complete

### Issue `ADW-S08-FE-01` – Macro event UI

- [ ] Issue complete
- Depends on: `T08-05`
- Subtasks:
  - [ ] `T08-07` Extend feed/timeline labels cho macro event categories
  - [ ] `T08-08` Add filters và impact badges tối thiểu cho macro events

## Verification Checklist

- [ ] Variety event tăng mà invalid spike vẫn trong ngưỡng
- [ ] Trade/ecology/scarcity tạo chain hậu quả giải thích được
- [ ] Observer surfaces vẫn readable sau expansion
