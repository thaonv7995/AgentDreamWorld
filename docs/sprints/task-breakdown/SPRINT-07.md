# Sprint 07 – Task Breakdown

## Breakdown Goal

Thêm cultural/mythic depth và era summaries đủ gọn để trở thành input context chính cho các sprint simulation mở rộng.

## Work Packages

- `WP1` Culture/Myth generation
- `WP2` Era summary compression
- `WP3` Projection/UI and context quality

## Atomic Tasks

| ID | Parent | Stream | Task | Depends On | Output |
| --- | --- | --- | --- | --- | --- |
| T07-01 | ADW-S07-BA-01 | BA | Chốt era summary schema, myth/culture taxonomy và acceptance criteria | None | summary + taxonomy contract |
| T07-02 | ADW-S07-BE-01 | Backend | Implement Culture agent qua runtime abstraction hiện có | T03-05,T07-01 | culture generation path |
| T07-03 | ADW-S07-BE-01 | Backend | Implement Myth agent qua runtime abstraction hiện có | T03-05,T07-01 | myth generation path |
| T07-04 | ADW-S07-BE-01 | Backend | Persist myth/culture outputs thành tags hoặc soft refs có thể query được | T07-02,T07-03 | culture/myth projections |
| T07-05 | ADW-S07-BE-01 | Backend | Implement era summary generator và compressed artifact persistence | T07-01,T07-04 | era summary artifacts |
| T07-06 | ADW-S07-BE-01 | Backend | Implement context selection rules ưu tiên era summaries thay cho raw history | T07-05 | bounded context path |
| T07-07 | ADW-S07-FE-01 | Frontend | Show culture/myth tags trên feed và overview surfaces | T07-04 | myth/culture UI tags |
| T07-08 | ADW-S07-FE-01 | Frontend | Add era summary panel và navigation states tối thiểu | T07-05,T07-06 | era summary UI |
| T07-09 | ADW-S07-DO-01 | DevOps | Version prompt/rule sets cho culture/myth path | T07-02,T07-03 | versioned prompt assets |
| T07-10 | ADW-S07-DO-01 | DevOps | Soak era transition path và đo token/context savings | T07-06,T07-08,T07-09 | context savings report |

## Suggested Sequence

1. `T07-01`
2. `T07-02` + `T07-03`
3. `T07-04 -> T07-05 -> T07-06`
4. `T07-07` + `T07-08`
5. `T07-09 -> T07-10`

## Cut Line

- Must-have: `T07-01..T07-08`
- Can defer: `T07-09..T07-10` reporting depth

## Verification Artifacts

- Era summaries đủ để replace phần lớn raw-history context
- Feed/world overview đã có myth/culture surface đọc được
- Era transition không gây context regression lớn
