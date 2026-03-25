# AI Dreams World – Master Backlog

Tài liệu này là backlog điều phối cấp sprint cho toàn dự án.

Mục đích:

- gom các work item chính theo sprint vào một chỗ
- gán `role owner`, `suggested owner`, `estimate`, `status`
- dùng như nguồn nhập tay sang Jira / Linear / Notion nếu cần

---

## Status Legend

- `Not Started`
- `In Progress`
- `Blocked`
- `At Risk`
- `Done`

## Estimate Legend

- `XS` = <= 0.5 ngày
- `S` = 1 ngày
- `M` = 2–3 ngày
- `L` = 4–5 ngày
- `XL` = > 5 ngày hoặc cần tách nhỏ thêm

---

## Sprint 00 – Repo Scaffold & Delivery Rails

| ID | Title | Role | Suggested Owner | Estimate | Status | Dependency | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- |
| ADW-S00-BA-01 | Chốt acceptance criteria cho repo scaffold | BA | BA Lead | S | Not Started | None | Bao gồm onboarding path và DoR cho Sprint 01 |
| ADW-S00-BE-01 | Tạo Rust workspace và binary `ai-dreams-server` | Backend | Backend Lead | M | Not Started | None | Kèm health/stub endpoint |
| ADW-S00-FE-01 | Tạo React + Vite app shell | Frontend | Frontend Lead | M | Not Started | None | Kèm layout shell và API stub |
| ADW-S00-DO-01 | Thiết lập `dev.sh`, `.env.example`, CI tối thiểu | DevOps | DevOps Lead | M | Not Started | None | Chốt commands local dev |

## Sprint 01 – World Model, SQLite Schema, Persistence

| ID | Title | Role | Suggested Owner | Estimate | Status | Dependency | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- |
| ADW-S01-BA-01 | Chốt glossary entity và contract `GET /worlds/current` | BA | BA Lead | S | Not Started | ADW-S00-BA-01 | Khóa `Region` và `Settlement` |
| ADW-S01-BE-01 | Implement schema SQLite V1 và migration/init flow | Backend | Backend Lead | L | Not Started | ADW-S00-BE-01 | Bao gồm worlds, regions, locations, civilizations, settlements, events |
| ADW-S01-FE-01 | Tạo world summary types và overview shell | Frontend | Frontend Lead | S | Not Started | ADW-S01-BA-01 | Có empty state |
| ADW-S01-DO-01 | Thêm smoke test cho DB init và seed path | DevOps | DevOps Lead | S | Not Started | ADW-S01-BE-01 | Kèm chuẩn hóa `data/` path |

## Sprint 02 – Event Pipeline, Tick Runner, Guardian/Historian

| ID | Title | Role | Suggested Owner | Estimate | Status | Dependency | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- |
| ADW-S02-BA-01 | Chốt event lifecycle và raw/canonical rules | BA | BA Lead | S | Not Started | ADW-S01-BA-01 | Chốt contract tick endpoint |
| ADW-S02-BE-01 | Implement event pipeline và manual tick | Backend | Backend Lead | L | Not Started | ADW-S01-BE-01 | EventProposal, append-only log, tick orchestrator |
| ADW-S02-FE-01 | Tạo debug tick trigger và event list shell | Frontend | Frontend Lead | S | Not Started | ADW-S02-BE-01 | Phục vụ demo và test |
| ADW-S02-DO-01 | Thêm logs, env flags, smoke test cho tick lifecycle | DevOps | DevOps Lead | S | Not Started | ADW-S02-BE-01 | Mock/live mode |

## Sprint 03 – Genesis Mode & 3 Creative Agents V1

| ID | Title | Role | Suggested Owner | Estimate | Status | Dependency | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- |
| ADW-S03-BA-01 | Chốt acceptance criteria cho Genesis và quality rubric 3 agents V1 | BA | BA Lead | S | Not Started | ADW-S02-BA-01 | Chốt data tối thiểu sau genesis |
| ADW-S03-BE-01 | Implement Creator, Civilization, Storyteller và Genesis runner | Backend | Backend Lead | XL | Not Started | ADW-S02-BE-01 | Áp boundaries vào bootstrap |
| ADW-S03-FE-01 | Render event/world data thật sau genesis | Frontend | Frontend Lead | M | Not Started | ADW-S03-BE-01 | Có loading state và filter shell |
| ADW-S03-DO-01 | Thiết lập provider profiles, retry/timeout, smoke genesis run | DevOps | DevOps Lead | M | Not Started | ADW-S03-BE-01 | Mock/live |

## Sprint 04 – Dream Feed & World Overview UI

| ID | Title | Role | Suggested Owner | Estimate | Status | Dependency | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- |
| ADW-S04-BA-01 | Chốt observer-mode UX và filter behavior | BA | BA Lead | S | Not Started | ADW-S03-BA-01 | Chốt information hierarchy |
| ADW-S04-BE-01 | Tối ưu event/world queries cho UI vertical slice | Backend | Backend Lead | M | Not Started | ADW-S03-BE-01 | Feed + overview |
| ADW-S04-FE-01 | Implement Dream Feed và World Overview UI | Frontend | Frontend Lead | L | Not Started | ADW-S04-BE-01 | Kèm polling/refresh |
| ADW-S04-DO-01 | Thêm preview build và CI app-shell flow | DevOps | DevOps Lead | S | Not Started | ADW-S04-FE-01 | Hỗ trợ demo |

## Sprint 05 – Timeline, Simulation Controls, God Mode Lite

| ID | Title | Role | Suggested Owner | Estimate | Status | Dependency | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- |
| ADW-S05-BA-01 | Chốt UX timeline và preset God Mode V1 | BA | BA Lead | S | Not Started | ADW-S04-BA-01 | Chốt rule hậu quả tối thiểu |
| ADW-S05-BE-01 | Implement timeline projection, controls, God Mode lite | Backend | Backend Lead | L | Not Started | ADW-S04-BE-01 | Pause/resume/manual tick + preset endpoints |
| ADW-S05-FE-01 | Implement Timeline UI và simulation controls | Frontend | Frontend Lead | L | Not Started | ADW-S05-BE-01 | Kèm panel God Mode lite |
| ADW-S05-DO-01 | Chuẩn bị staging/demo profile cho timeline + God Mode | DevOps | DevOps Lead | S | Not Started | ADW-S05-BE-01 | Kèm replay demo commands |

## Sprint 06 – Export, Single-Binary Mode, MVP Hardening

| ID | Title | Role | Suggested Owner | Estimate | Status | Dependency | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- |
| ADW-S06-BA-01 | Chốt format export và sign-off MVP DoD | BA | BA Lead | S | Not Started | ADW-S05-BA-01 | Bao gồm scope cut cuối MVP |
| ADW-S06-BE-01 | Implement wiki/annals export và backend serve static frontend | Backend | Backend Lead | L | Not Started | ADW-S05-BE-01 | Kèm hardening config/error handling |
| ADW-S06-FE-01 | Implement export UI và polish MVP path | Frontend | Frontend Lead | M | Not Started | ADW-S06-BE-01 | Loại bỏ mock-only UX |
| ADW-S06-DO-01 | Tạo release pipeline single-binary và smoke export flow | DevOps | DevOps Lead | M | Not Started | ADW-S06-BE-01 | Kèm artifact naming/release checklist |

## Sprint 07 – Culture, Myth, Era Summaries

| ID | Title | Role | Suggested Owner | Estimate | Status | Dependency | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- |
| ADW-S07-BA-01 | Chốt acceptance criteria cho Culture/Myth và schema era summary | BA | BA Lead | S | Not Started | ADW-S06-BA-01 | Tạo lore quality rubric |
| ADW-S07-BE-01 | Implement Culture Agent, Myth Agent, era summaries | Backend | Backend Lead | XL | Not Started | ADW-S06-BE-01 | Kèm summary storage/access |
| ADW-S07-FE-01 | Hiển thị culture/myth tags và era summary panel | Frontend | Frontend Lead | M | Not Started | ADW-S07-BE-01 | Chuẩn bị data model cho Mythology Browser |
| ADW-S07-DO-01 | Theo dõi token cost và soak era transition | DevOps | DevOps Lead | S | Not Started | ADW-S07-BE-01 | Version prompts/rules |

## Sprint 08 – Ecology, Economy, Chaos, Macro Rules

| ID | Title | Role | Suggested Owner | Estimate | Status | Dependency | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- |
| ADW-S08-BA-01 | Chốt macro rules và coherence metrics cho expanded simulation | BA | BA Lead | S | Not Started | ADW-S07-BA-01 | Focus reject rate, scarcity/conflict chains |
| ADW-S08-BE-01 | Implement Ecology, Economy, Chaos và propagation rules | Backend | Backend Lead | XL | Not Started | ADW-S07-BE-01 | Kèm Guardian expansion |
| ADW-S08-FE-01 | Mở rộng feed/timeline cho event types mới | Frontend | Frontend Lead | S | Not Started | ADW-S08-BE-01 | Impact labels và filters |
| ADW-S08-DO-01 | Long-run simulation test và alert review | DevOps | DevOps Lead | M | Not Started | ADW-S08-BE-01 | Theo dõi budget/tick và instability |

## Sprint 09 – Region Map & Civilization Viewer

| ID | Title | Role | Suggested Owner | Estimate | Status | Dependency | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- |
| ADW-S09-BA-01 | Chốt UX map beta và content bắt buộc của Civilization Viewer | BA | BA Lead | S | Not Started | ADW-S08-BA-01 | Chốt territory/ownership display |
| ADW-S09-BE-01 | Implement map projection, territory ownership, civ detail projection | Backend | Backend Lead | L | Not Started | ADW-S08-BE-01 | Phục vụ map + detail |
| ADW-S09-FE-01 | Implement region map beta và Civilization Viewer | Frontend | Frontend Lead | XL | Not Started | ADW-S09-BE-01 | Kèm cross-link từ feed/timeline |
| ADW-S09-DO-01 | Thiết lập perf budget và preview deployment cho visual QA | DevOps | DevOps Lead | S | Not Started | ADW-S09-FE-01 | Chuẩn bị demo snapshots |

## Sprint 10 – Mythology Browser & Knowledge Graph

| ID | Title | Role | Suggested Owner | Estimate | Status | Dependency | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- |
| ADW-S10-BA-01 | Chốt taxonomy Mythology Browser và use cases Knowledge Graph | BA | BA Lead | S | Not Started | ADW-S09-BA-01 | Chốt acceptance criteria entity linking |
| ADW-S10-BE-01 | Implement mythology projection và graph projection | Backend | Backend Lead | L | Not Started | ADW-S09-BE-01 | Link civ-religion-myth-event-region-settlement |
| ADW-S10-FE-01 | Implement Mythology Browser và Knowledge Graph beta | Frontend | Frontend Lead | XL | Not Started | ADW-S10-BE-01 | Kèm cross-navigation |
| ADW-S10-DO-01 | Theo dõi perf graph rendering và query latency | DevOps | DevOps Lead | S | Not Started | ADW-S10-FE-01 | Visual regression/demo checklist |

## Sprint 11 – Optional Advanced Infra & Observability

| ID | Title | Role | Suggested Owner | Estimate | Status | Dependency | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- |
| ADW-S11-BA-01 | Chốt non-goals và KPI/SLI cho advanced profile | BA | BA Lead | S | Not Started | ADW-S10-BA-01 | Giữ SQLite là default path |
| ADW-S11-BE-01 | Tách config profile và expose instrumentation layer | Backend | Backend Lead | L | Not Started | ADW-S10-BE-01 | Optional Postgres/Redis |
| ADW-S11-FE-01 | Thêm debug/admin health summary tối thiểu | Frontend | Frontend Lead | S | Not Started | ADW-S11-BE-01 | Không làm nhiễu user UI |
| ADW-S11-DO-01 | Thiết lập compose advanced profile và observability baseline | DevOps | DevOps Lead | L | Not Started | ADW-S11-BE-01 | Load/perf test, backup/restore baseline |

## Sprint 12 – Multi-world Foundation & Project Ops

| ID | Title | Role | Suggested Owner | Estimate | Status | Dependency | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- |
| ADW-S12-BA-01 | Chốt use cases multi-world, fork, snapshot metadata | BA | BA Lead | S | Not Started | ADW-S11-BA-01 | Review impact current-world UX |
| ADW-S12-BE-01 | Implement multi-world metadata model và snapshot/fork foundation | Backend | Backend Lead | XL | Not Started | ADW-S11-BE-01 | Kèm backward compatibility path |
| ADW-S12-FE-01 | Tạo world selector/world list shell | Frontend | Frontend Lead | M | Not Started | ADW-S12-BE-01 | Chuẩn bị future alternate timeline UX |
| ADW-S12-DO-01 | Tạo ops runbook và workflows backup/restore multi-world | DevOps | DevOps Lead | M | Not Started | ADW-S12-BE-01 | Monitoring for world growth |

