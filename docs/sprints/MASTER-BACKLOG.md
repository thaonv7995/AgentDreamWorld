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
| ADW-S02-BE-01 | Implement event pipeline và manual tick | Backend | Backend Lead | L | Not Started | ADW-S01-BE-01 | EventProposal, append-only log, tick orchestrator, `llm_call_log`, `tick_log` |
| ADW-S02-FE-01 | Tạo debug tick trigger và event list shell | Frontend | Frontend Lead | S | Not Started | ADW-S02-BE-01 | Phục vụ demo và test |
| ADW-S02-DO-01 | Thêm logs, env flags, smoke test cho tick lifecycle | DevOps | DevOps Lead | S | Not Started | ADW-S02-BE-01 | Mock/live mode, report path, top reject reasons |

## Sprint 03 – Genesis Mode & 3 Creative Agents V1

| ID | Title | Role | Suggested Owner | Estimate | Status | Dependency | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- |
| ADW-S03-BA-01 | Chốt acceptance criteria cho Genesis và quality rubric 3 agents V1 | BA | BA Lead | S | Not Started | ADW-S02-BA-01 | Chốt data tối thiểu sau genesis |
| ADW-S03-BE-01 | Implement Creator, Civilization, Storyteller và Genesis runner | Backend | Backend Lead | XL | Not Started | ADW-S02-BE-01 | Áp boundaries vào bootstrap, replay mode, API contract tests |
| ADW-S03-FE-01 | Render event/world data thật sau genesis | Frontend | Frontend Lead | M | Not Started | ADW-S03-BE-01 | Có loading state, filter shell, feed/timeline projection contract |
| ADW-S03-DO-01 | Thiết lập provider profiles, retry/timeout, smoke genesis run | DevOps | DevOps Lead | M | Not Started | ADW-S03-BE-01 | Mock/live, snapshot/replay verify |

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

## Sprint 11 – Optional Advanced Infra & Advanced Observability

| ID | Title | Role | Suggested Owner | Estimate | Status | Dependency | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- |
| ADW-S11-BA-01 | Chốt non-goals và KPI/SLI cho advanced profile | BA | BA Lead | S | Not Started | ADW-S10-BA-01 | Giữ SQLite là default path, không duplicate baseline observability |
| ADW-S11-BE-01 | Tách config profile và expose advanced instrumentation layer | Backend | Backend Lead | L | Not Started | ADW-S10-BE-01 | Optional Postgres/Redis, dùng lại `tick_log`/`llm_call_log` |
| ADW-S11-FE-01 | Thêm debug/admin health summary tối thiểu | Frontend | Frontend Lead | S | Not Started | ADW-S11-BE-01 | Không làm nhiễu user UI |
| ADW-S11-DO-01 | Thiết lập compose advanced profile và advanced observability stack | DevOps | DevOps Lead | L | Not Started | ADW-S11-BE-01 | Load/perf test, backup/restore baseline |

## Sprint 12 – Multi-world Foundation & Project Ops

| ID | Title | Role | Suggested Owner | Estimate | Status | Dependency | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- |
| ADW-S12-BA-01 | Chốt use cases multi-world, fork, snapshot metadata | BA | BA Lead | S | Not Started | ADW-S11-BA-01 | Review impact current-world UX |
| ADW-S12-BE-01 | Implement multi-world metadata model và snapshot/fork foundation | Backend | Backend Lead | XL | Not Started | ADW-S11-BE-01 | Kèm backward compatibility path |
| ADW-S12-FE-01 | Tạo world selector/world list shell | Frontend | Frontend Lead | M | Not Started | ADW-S12-BE-01 | Chuẩn bị future alternate timeline UX |
| ADW-S12-DO-01 | Tạo ops runbook và workflows backup/restore multi-world | DevOps | DevOps Lead | M | Not Started | ADW-S12-BE-01 | Monitoring for world growth |

## Sprint 13 – Multi-world Manager, Presets & World Lifecycle UX

| ID | Title | Role | Suggested Owner | Estimate | Status | Dependency | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- |
| ADW-S13-BA-01 | Chốt UX và lifecycle rules cho multi-world manager | BA | BA Lead | S | Not Started | ADW-S12-BA-01 | Bao gồm presets và archive states |
| ADW-S13-BE-01 | Implement world manager APIs, presets và state isolation | Backend | Backend Lead | XL | Not Started | ADW-S12-BE-01 | Create/select/archive, preset metadata |
| ADW-S13-FE-01 | Implement multi-world manager UI và world creation flow | Frontend | Frontend Lead | L | Not Started | ADW-S13-BE-01 | Current-world path vẫn phải rõ |
| ADW-S13-DO-01 | Thiết lập ops checks cho nhiều world active/archive | DevOps | DevOps Lead | M | Not Started | ADW-S13-BE-01 | Storage growth, backup naming |

## Sprint 14 – Pace Control, Event Log Viewer & Config Inspector

| ID | Title | Role | Suggested Owner | Estimate | Status | Dependency | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- |
| ADW-S14-BA-01 | Chốt control semantics cho pace/fast-forward và inspector UX | BA | BA Lead | S | Not Started | ADW-S13-BA-01 | Slow/Normal/Fast, +50/+100/+1 era |
| ADW-S14-BE-01 | Implement pace control, fast-forward, log/config projections | Backend | Backend Lead | XL | Not Started | ADW-S13-BE-01 | Per-world runtime state, inspector payloads |
| ADW-S14-FE-01 | Implement pace controls, Event Log Viewer, Config Inspector | Frontend | Frontend Lead | XL | Not Started | ADW-S14-BE-01 | Kèm filters và debug views |
| ADW-S14-DO-01 | Tạo verification flow cho fast-forward, pacing và inspection metrics | DevOps | DevOps Lead | M | Not Started | ADW-S14-BE-01 | Soak runs theo nhiều pace |

## Sprint 15 – Advanced God Mode & Story Arc Highlighter

| ID | Title | Role | Suggested Owner | Estimate | Status | Dependency | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- |
| ADW-S15-BA-01 | Chốt guardrails cho Advanced God Mode và taxonomy story arcs | BA | BA Lead | S | Not Started | ADW-S14-BA-01 | Scope/intensity rules, arc categories |
| ADW-S15-BE-01 | Implement advanced interventions và story arc extraction | Backend | Backend Lead | XL | Not Started | ADW-S14-BE-01 | Guardrails, arc scoring, traceability |
| ADW-S15-FE-01 | Implement Advanced God Mode UI và story arc surfaces | Frontend | Frontend Lead | L | Not Started | ADW-S15-BE-01 | Kèm previews, arc cards, cross-links |
| ADW-S15-DO-01 | Chạy coherence/cost review cho advanced intervention paths | DevOps | DevOps Lead | M | Not Started | ADW-S15-BE-01 | Detect intervention instability |

## Sprint 16 – World Forking, Alternate Timeline Compare & Snapshot Sharing

| ID | Title | Role | Suggested Owner | Estimate | Status | Dependency | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- |
| ADW-S16-BA-01 | Chốt UX fork/compare và provenance rules cho snapshots | BA | BA Lead | S | Not Started | ADW-S15-BA-01 | Chốt branch naming, compare semantics |
| ADW-S16-BE-01 | Implement world forking, branch compare và snapshot sharing | Backend | Backend Lead | XL | Not Started | ADW-S15-BE-01 | Fork at year/era/event checkpoint |
| ADW-S16-FE-01 | Implement alternate timeline UX và snapshot share flow | Frontend | Frontend Lead | XL | Not Started | ADW-S16-BE-01 | Diff summaries, branch navigation |
| ADW-S16-DO-01 | Tạo storage/recovery policy cho forks và snapshots | DevOps | DevOps Lead | M | Not Started | ADW-S16-BE-01 | Retention, restore, provenance checks |

## Sprint 17 – Per-agent Model Profiles, Local LLM & Multi-provider Settings

| ID | Title | Role | Suggested Owner | Estimate | Status | Dependency | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- |
| ADW-S17-BA-01 | Chốt profile matrix và user-facing settings model cho providers | BA | BA Lead | S | Not Started | ADW-S16-BA-01 | Global vs per-agent-group |
| ADW-S17-BE-01 | Implement per-agent profiles, local LLM path và provider routing | Backend | Backend Lead | XL | Not Started | ADW-S16-BE-01 | OpenAI/Perplexity/local compatibility |
| ADW-S17-FE-01 | Implement provider settings UI và runtime profile inspection | Frontend | Frontend Lead | L | Not Started | ADW-S17-BE-01 | Kèm default-safe path |
| ADW-S17-DO-01 | Thiết lập provider smoke matrix và local profile ops notes | DevOps | DevOps Lead | M | Not Started | ADW-S17-BE-01 | Health checks, fallback tests |

## Sprint 18 – Myths Export, Highlight Packs & Creator Publishing Pipeline

| ID | Title | Role | Suggested Owner | Estimate | Status | Dependency | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- |
| ADW-S18-BA-01 | Chốt creator pack format cho myths/arcs/highlights | BA | BA Lead | S | Not Started | ADW-S17-BA-01 | Bao gồm output acceptance và naming |
| ADW-S18-BE-01 | Implement myths export, highlight manifests và publishing bundles | Backend | Backend Lead | XL | Not Started | ADW-S17-BE-01 | Optional remote artifact path |
| ADW-S18-FE-01 | Implement creator export UI và artifact browsing flow | Frontend | Frontend Lead | L | Not Started | ADW-S18-BE-01 | Packs, previews, download states |
| ADW-S18-DO-01 | Thiết lập artifact retention và publish/storage workflow | DevOps | DevOps Lead | M | Not Started | ADW-S18-BE-01 | Remote storage optional path |

## Sprint 19 – Community Worlds, Package Export/Import & Shared Gallery

| ID | Title | Role | Suggested Owner | Estimate | Status | Dependency | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- |
| ADW-S19-BA-01 | Chốt world package spec, provenance fields và gallery UX | BA | BA Lead | S | Not Started | ADW-S18-BA-01 | Bao gồm moderation metadata |
| ADW-S19-BE-01 | Implement package export/import, versioning và shared gallery APIs | Backend | Backend Lead | XL | Not Started | ADW-S18-BE-01 | Seed + history + metadata |
| ADW-S19-FE-01 | Implement community gallery và import/export flows | Frontend | Frontend Lead | XL | Not Started | ADW-S19-BE-01 | Browse/filter/provenance surfaces |
| ADW-S19-DO-01 | Tạo moderation/runbook và package compatibility checks | DevOps | DevOps Lead | M | Not Started | ADW-S19-BE-01 | Trust, review, schema compatibility |

## Sprint 20 – Collaborative Viewing, Shared Sessions & Social Safety Rails

| ID | Title | Role | Suggested Owner | Estimate | Status | Dependency | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- |
| ADW-S20-BA-01 | Chốt session roles, permissions và safety rails cho collab mode | BA | BA Lead | S | Not Started | ADW-S19-BA-01 | Viewer/operator/moderator model |
| ADW-S20-BE-01 | Implement shared session runtime, audit trail và intervention conflict handling | Backend | Backend Lead | XL | Not Started | ADW-S19-BE-01 | Collaborative viewing không biến thành MMO backend |
| ADW-S20-FE-01 | Implement collaborative viewing UI, presence và shared control states | Frontend | Frontend Lead | XL | Not Started | ADW-S20-BE-01 | Feed/timeline/session state sync |
| ADW-S20-DO-01 | Thiết lập ops, rate-limit và abuse/runbook cho collaborative sessions | DevOps | DevOps Lead | M | Not Started | ADW-S20-BE-01 | Session safety và rollback path |
