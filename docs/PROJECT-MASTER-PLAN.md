# AI Dreams World – Project Master Plan

Tài liệu này là **master control document** để theo dõi tiến độ triển khai AI Dreams World sau khi đã có spec và implementation plan.

Nó dùng để:

- kiểm soát phase và sprint
- theo dõi milestone
- phát hiện rủi ro sớm
- giữ project không trượt khỏi MVP
- tạo nhịp báo cáo rõ cho tech lead / PM / founder

Checklist vận hành theo từng sprint nằm trong `docs/sprints/README.md`.
Backlog điều phối theo sprint/role/estimate/status nằm trong `docs/sprints/MASTER-BACKLOG.md`.

---

## 1. Current Project Status

| Hạng mục | Trạng thái hiện tại |
| --- | --- |
| Product docs | Hoàn thành baseline |
| Implementation plan | Có |
| Master plan | Có |
| Code scaffold | Chưa bắt đầu |
| MVP build | Chưa bắt đầu |
| Release candidate | Chưa bắt đầu |

Current active target:

- **Bắt đầu ở Phase 0 / Sprint 0**
- Ưu tiên cao nhất: chuyển repo từ `docs-only` sang runnable scaffold

---

## 2. Governance Model

### 2.1 Cadence chuẩn

- Sprint length: **2 tuần**
- Planning: đầu sprint
- Mid-sprint checkpoint: giữa sprint
- Sprint demo: cuối sprint
- Retro + replan: sau demo

### 2.2 Status values

- `Not Started`
- `In Progress`
- `At Risk`
- `Blocked`
- `Done`

### 2.3 Control principle

- Không đưa feature V2/V3 vào trước khi MVP gate đạt, trừ khi đó là unblocker kỹ thuật rõ ràng.
- Mọi thay đổi milestone phải cập nhật doc này trước khi team commit scope mới.
- Nếu bất kỳ milestone nào trượt quá **1 sprint**, bắt buộc mở replan chính thức.

---

## 3. Master Roadmap Dashboard

| Phase | Sprint range | Goal | Main outputs | Gate | Status |
| --- | --- | --- | --- | --- | --- |
| Phase 0 – Foundation | Sprint 0 | Runnable scaffold | Rust server shell, React shell, scripts, env | Gate A | Not Started |
| Phase 1 – Engine Foundation | Sprint 1–2 | World model + tick engine | SQLite schema, event pipeline, manual tick | Gate B | Not Started |
| Phase 2 – MVP Vertical Slice | Sprint 3–4 | First usable world experience | Genesis, Dream Feed, World Overview | Gate C | Not Started |
| Phase 3 – MVP RC | Sprint 5–6 | Release candidate | Timeline, export, single-binary, QA | Gate D | Not Started |
| Phase 4 – Expanded Simulation | Sprint 7–8 | V2 simulation richness | Culture/Myth/Ecology/Economy/Chaos | Gate E | Not Started |
| Phase 5 – Visualization | Sprint 9–10 | Deeper exploration | Map, Civilization Viewer, Graph | Gate F | Not Started |
| Phase 6 – Platform Expansion | Sprint 11–12 | Scale path | optional infra, advanced observability, multi-world foundation | Gate G | Not Started |

---

## 4. Milestone Gates

| Gate | Target sprint | Definition |
| --- | --- | --- |
| Gate A – Scaffold Ready | Sprint 0 | Repo có backend/frontend skeleton chạy được |
| Gate B – Engine Foundation Ready | Sprint 2 | World model + persistence + event/tick pipeline ổn định |
| Gate C – MVP Vertical Slice Ready | Sprint 4 | User quan sát được world thật qua Dream Feed + World Overview |
| Gate D – MVP Release Candidate | Sprint 6 | Đạt DoD của V1 trong `MVP-SPEC.md` |
| Gate E – Expanded Simulation Ready | Sprint 8 | Thêm agents V2 mà vẫn giữ coherence |
| Gate F – Visualization Ready | Sprint 10 | Map + Civilization Viewer + Mythology/Graph usable |
| Gate G – Platform Expansion Ready | Sprint 12 | Optional advanced infra + advanced observability + multi-world foundation có đường chạy |

---

## 5. Sprint Control Board

Sử dụng bảng này như tracker cập nhật sau mỗi sprint.

| Sprint | Phase | Sprint goal | Planned features | Demo output | Status | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| Sprint 0 | Foundation | Repo scaffold | backend shell, frontend shell, dev scripts, **process modes, walking skeleton** | stub app chạy được | Not Started | |
| Sprint 1 | Engine Foundation | World model + schema | **7 core tables**, migrations, repositories, **db-per-world** | seeded world summary | Not Started | |
| Sprint 2 | Engine Foundation | Tick pipeline | event log, **declarative Guardian**, **scoring Historian**, manual tick, **llm_call_log, tick_log, CLI report, mock provider, error classification** | 1 tick end-to-end | Not Started | |
| Sprint 3 | MVP Vertical Slice | Genesis + agents | Creator, Civilization, Storyteller, **API contract types, contract tests, snapshot testing** | generated world | Not Started | |
| Sprint 4 | MVP Vertical Slice | First observer UI | Dream Feed, World Overview | usable MVP slice | Not Started | |
| Sprint 5 | MVP RC | Timeline + controls | timeline, pause/resume, God Mode lite | history navigation | Not Started | |
| Sprint 6 | MVP RC | Export + hardening | wiki, annals, single-binary, QA | MVP RC demo | Not Started | |
| Sprint 7 | Expanded Simulation | Culture + Myth | era summaries, myth/culture | richer lore demo | Not Started | |
| Sprint 8 | Expanded Simulation | Ecology + Economy + Chaos | scarcity/conflict rules | simulation depth demo | Not Started | |
| Sprint 9 | Visualization | Map + civ detail | map beta, civilization viewer | visual exploration | Not Started | |
| Sprint 10 | Visualization | Mythology + graph | browser, graph beta | lore graph demo | Not Started | |
| Sprint 11 | Platform Expansion | Advanced profile | Postgres/Redis optional, advanced observability | ops/perf demo | Not Started | |
| Sprint 12 | Platform Expansion | Multi-world foundation | fork/snapshot/gallery metadata | multi-world demo | Not Started | |

---

## 6. KPI Dashboard

### 6.1 Delivery KPIs

| KPI | Target | Review cadence | Owner role |
| --- | --- | --- | --- |
| Sprint commitment completion | >= 80% | End sprint | Project lead |
| Milestone slip | <= 1 sprint | Weekly | Project lead |
| Blocker age | < 3 working days | Weekly | Tech lead |
| Demo readiness | 100% sprints có demo | End sprint | All leads |

### 6.2 Product / Simulation KPIs

| KPI | Target | Review cadence | Owner role |
| --- | --- | --- | --- |
| Tick success rate | >= 95% | Weekly | Backend lead |
| Guardian reject rate | Có lý do rõ, không spike bất thường | Weekly | Agent/runtime lead |
| Canonical event quality review | >= 80% event đạt chuẩn coherence | End sprint | Product + runtime |
| World bootstrap time | < 2 phút cho world đầu tiên | End sprint | Backend lead |
| Export success rate | >= 95% | End sprint | Export owner |

### 6.3 Quality KPIs

| KPI | Target | Review cadence | Owner role |
| --- | --- | --- | --- |
| Build green rate | >= 90% | Weekly | DevEx owner |
| Regression bugs mở cuối sprint | 0 blocker | End sprint | QA/tech lead |
| Docs drift count | 0 conflict nghiêm trọng giữa code và docs | End sprint | Project lead |
| Setup success for new contributor | < 30 phút tới first run | Mỗi gate lớn | DevEx owner |

### 6.4 Cost / Runtime KPIs

| KPI | Target | Review cadence | Owner role |
| --- | --- | --- | --- |
| Token cost / tick | Trong ngân sách team chấp nhận | Weekly | Runtime owner |
| Avg tick duration | Ổn định theo phase target | Weekly | Backend lead |
| Summary compression effectiveness | Agent context không phình mất kiểm soát | Sprint review | Runtime owner |

---

## 7. Risk Register

| Risk | Tác động | Xác suất | Dấu hiệu sớm | Mitigation | Status |
| --- | --- | --- | --- | --- | --- |
| Docs-code drift sau khi scaffold | Cao | Cao | README/DEV-SETUP không còn chạy đúng | Review docs mỗi sprint, cập nhật song song với code | Open |
| Scope creep từ V2/V3 trước MVP | Cao | Cao | Sprint backlog chứa map/graph trước MVP gate | Enforce gate D trước advanced scope | Open |
| LLM cost/latency quá cao | Cao | Trung bình | Tick time tăng mạnh, budget khó kiểm soát | **Structured tick log + cost alert từ Sprint 2**, mock mode, summaries, model tiering. Xem [LIMITATIONS.md](LIMITATIONS.md) §M5 | Open |
| Simulation incoherence | Cao | Trung bình | Guardian reject rate cao, lore mâu thuẫn | **Declarative rule engine + composable validators từ Sprint 2**, test fixtures, tune prompts. Xem [LIMITATIONS.md](LIMITATIONS.md) §M2 | Open |
| Non-deterministic pipeline khó debug | Cao | Cao | Bug không rõ thuộc layer nào | **Record/replay (`llm_call_log`) + error classification (`PipelineStage`) + mock provider + snapshot testing từ Sprint 2**. Xem [LIMITATIONS.md](LIMITATIONS.md) §M1 | Open |
| Schema churn do vocabulary chưa ổn | Trung bình | Trung bình | Migration đổi liên tục | **Slim schema V1 (7 core tables), soft references cho entities chưa cần table, schema version tracking**. Xem [LIMITATIONS.md](LIMITATIONS.md) §M4 | Open |
| Frontend-backend contract drift | Trung bình | Cao | UI build trên assumptions sai | **API contract types (TypeScript) + contract tests trước Sprint 4**. Xem [LIMITATIONS.md](LIMITATIONS.md) §M6 | Open |
| Frontend đi nhanh hơn engine | Trung bình | Cao | UI có nhiều mock hơn real data | Ưu tiên vertical slice thật thay vì UI fake | Open |
| Single maintainer bottleneck | Cao | Trung bình | Sprint slip liên tiếp | Chia workstreams rõ, giảm WIP, ưu tiên MVP | Open |
| Monolith coupling khó isolate lỗi | Trung bình | Trung bình | Lỗi provider làm nhiễu toàn app | **Process modes + tokio task isolation + channel-based sim control từ Sprint 0**. Xem [LIMITATIONS.md](LIMITATIONS.md) §M3 | Open |

---

## 8. Decision Log Rules

Mọi quyết định làm đổi scope, architecture, hoặc milestone phải ghi theo format này:

| Date | Decision | Why | Impacted docs/files | Owner |
| --- | --- | --- | --- | --- |
| YYYY-MM-DD | Ví dụ: chuyển sprint 5 sang ưu tiên export trước God Mode | unblock demo gate D | IMPLEMENTATION-PLAN.md, MVP-SPEC.md | Project lead |

---

## 9. Weekly Reporting Template

### Weekly Status

- Phase hiện tại:
- Sprint hiện tại:
- Traffic light:
- Điểm đã hoàn thành tuần này:
- Blockers:
- Risk mới:
- Decision cần chốt:
- Dự kiến demo cuối sprint:

### Required Attachments

- Link branch / PR / changelog
- Screenshot hoặc demo notes
- KPI snapshot
- Doc changes nếu có

---

## 10. Sprint Review Checklist

Cuối mỗi sprint phải trả lời được:

- Sprint goal có đạt không?
- Demo có thể hiện tính năng thật hay chỉ mock?
- Có blocker nào carry over không?
- Có scope nào cần cắt để giữ milestone kế tiếp không?
- Docs nào cần cập nhật để phản ánh trạng thái mới?
- Gate hiện tại đã pass chưa, hay còn điều kiện treo?

---

## 11. Replan Triggers

Phải mở replan nếu gặp một trong các điều kiện sau:

- Trượt milestone quá 1 sprint.
- Tick success rate xuống dưới ngưỡng chấp nhận trong 2 sprint liên tiếp.
- MVP scope bị đòi nới rộng ngoài `MVP-SPEC.md`.
- Chi phí LLM/runtime vượt ngân sách dự kiến.
- Team capacity thay đổi đáng kể.

Khi replan, bắt buộc cập nhật đồng thời:

- `IMPLEMENTATION-PLAN.md`
- `PROJECT-MASTER-PLAN.md`
- `roadmap.md` nếu roadmap horizon thay đổi
- `MVP-SPEC.md` nếu Definition of Done hoặc phạm vi V1 thay đổi
