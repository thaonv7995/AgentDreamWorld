# AI Dreams World – Sprint Library

Thư mục này tách `IMPLEMENTATION-PLAN.md` thành các file nhỏ hơn theo từng sprint để dễ:

- giao việc
- tracking hằng tuần
- update tiến độ theo role
- dùng làm working doc trong sprint planning

---

## Cách dùng

- Mỗi sprint có 1 file riêng theo format **BA sprint document**.
- Mỗi sprint cũng có 1 file companion trong `implementation/` để chốt hướng thực thi kỹ thuật.
- Mỗi sprint cũng có 1 file companion trong `task-breakdown/` để bẻ nhỏ thành atomic tasks.
- Mỗi sprint cũng có 1 file companion trong `issue-ready/` để team tick execution theo `Epic -> Issue -> Subtask`.
- Checklist được chia theo 4 role chính:
  - `BA`
  - `Backend`
  - `Frontend`
  - `DevOps`
- Mỗi file sprint nên được dùng như tài liệu planning chính trong sprint đó.
- Mỗi file sprint có các phần chuẩn:
  - `Sprint Metadata`
  - `Sprint Goal`
  - `Business Objective`
  - `Business Value`
  - `In Scope`
  - `Out of Scope`
  - `Primary User Stories`
  - `Acceptance Criteria`
  - `Dependencies`
  - `Sprint Task Board`
  - `Risks & Control Notes`
  - checklist theo role
  - `Demo & Sign-off`
- Nếu task đã xong, tick `[x]`.
- `Sprint Task Board` phải mirror lại task IDs từ `MASTER-BACKLOG.md`.
- Checklist theo role phải đủ atomic để giao việc trực tiếp, ưu tiên format mã bước như `BA-03.1`, `BE-03.2`.
- Nếu scope đổi, cập nhật:
  - file sprint tương ứng
  - `IMPLEMENTATION-PLAN.md`
  - `PROJECT-MASTER-PLAN.md` nếu milestone/risk đổi

---

## Sprint Index

| Sprint | Goal | File |
| --- | --- | --- |
| Sprint 00 | Repo scaffold và execution rails | `SPRINT-00.md` |
| Sprint 01 | World model, SQLite schema, persistence | `SPRINT-01.md` |
| Sprint 02 | Event pipeline, tick runner, Guardian/Historian | `SPRINT-02.md` |
| Sprint 03 | Genesis mode và 3 creative agents V1 | `SPRINT-03.md` |
| Sprint 04 | Dream Feed và World Overview UI | `SPRINT-04.md` |
| Sprint 05 | Timeline, simulation controls, God Mode lite | `SPRINT-05.md` |
| Sprint 06 | Export, single-binary mode, MVP hardening | `SPRINT-06.md` |
| Sprint 07 | Culture, Myth, era summaries | `SPRINT-07.md` |
| Sprint 08 | Ecology, Economy, Chaos, macro rules | `SPRINT-08.md` |
| Sprint 09 | Region map và Civilization Viewer | `SPRINT-09.md` |
| Sprint 10 | Mythology Browser và Knowledge Graph | `SPRINT-10.md` |
| Sprint 11 | Optional advanced infra và advanced observability | `SPRINT-11.md` |
| Sprint 12 | Multi-world foundation và project ops | `SPRINT-12.md` |
| Sprint 13 | Multi-world manager, presets và lifecycle UX | `SPRINT-13.md` |
| Sprint 14 | Pace control, event log viewer và config inspector | `SPRINT-14.md` |
| Sprint 15 | Advanced God Mode và Story Arc Highlighter | `SPRINT-15.md` |
| Sprint 16 | World forking, alternate timeline compare và snapshot sharing | `SPRINT-16.md` |
| Sprint 17 | Per-agent model profiles, local LLM và multi-provider settings | `SPRINT-17.md` |
| Sprint 18 | Myths export, highlight packs và creator publishing pipeline | `SPRINT-18.md` |
| Sprint 19 | Community worlds, package export/import và shared gallery | `SPRINT-19.md` |
| Sprint 20 | Collaborative viewing, shared sessions và social safety rails | `SPRINT-20.md` |

---

## Delivery Tracker

- Backlog tổng theo sprint/role/estimate/status: `MASTER-BACKLOG.md`
- Mỗi file sprint phải tham chiếu lại task IDs tương ứng từ backlog tổng.
- Implementation companions: `implementation/README.md`
- Task breakdown companions: `task-breakdown/README.md`
- Issue-ready execution boards: `issue-ready/README.md`

---

## Template

- File mẫu cho cấu trúc BA sprint document: `TEMPLATE-BA-SPRINT.md`

---

## Update Rule

Cuối mỗi sprint, bắt buộc cập nhật tối thiểu:

- trạng thái checklist
- deliverables đã đạt
- blocker carry-over
- quyết định đổi scope nếu có
- sign-off checklist và risk status của sprint
