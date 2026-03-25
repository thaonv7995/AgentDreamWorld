# AI Dreams World – Issue-Ready Sprint Boards

Thư mục này chứa lớp doc để đi từ sprint planning sang execution thực tế.

Mỗi file dùng format:

- `Epic` = work package cấp sprint
- `Issue` = backlog item `ADW-SXX-*`
- `Subtask` = atomic task `TXX-*`

Quy ước tick:

- Tick subtask: đổi `- [ ]` thành `- [x]` khi làm xong thật
- Tick issue: chỉ tick khi tất cả subtasks của issue đã xong
- Tick epic: chỉ tick khi tất cả issues trong epic đã xong

Nguồn truth theo lớp:

- `docs/sprints/SPRINT-XX.md`: planning / BA sprint doc
- `docs/sprints/implementation/SPRINT-XX.md`: implementation companion
- `docs/sprints/task-breakdown/SPRINT-XX.md`: work packages + atomic tasks
- `docs/sprints/issue-ready/SPRINT-XX.md`: execution board có checkbox

Rule khi update:

- Nếu task xong trong execution board, update luôn status tương ứng ở `MASTER-BACKLOG.md`
- Nếu task bị tách nhỏ thêm trong lúc làm, thêm subtask mới ngay dưới issue tương ứng
- Nếu scope đổi, sync lại `SPRINT-XX.md`, `task-breakdown/SPRINT-XX.md`, và file issue-ready cùng sprint

Index:

| Sprint | Issue-Ready Board |
| --- | --- |
| Sprint 00 | `SPRINT-00.md` |
| Sprint 01 | `SPRINT-01.md` |
| Sprint 02 | `SPRINT-02.md` |
| Sprint 03 | `SPRINT-03.md` |
| Sprint 04 | `SPRINT-04.md` |
| Sprint 05 | `SPRINT-05.md` |
| Sprint 06 | `SPRINT-06.md` |
| Sprint 07 | `SPRINT-07.md` |
| Sprint 08 | `SPRINT-08.md` |
| Sprint 09 | `SPRINT-09.md` |
| Sprint 10 | `SPRINT-10.md` |
| Sprint 11 | `SPRINT-11.md` |
| Sprint 12 | `SPRINT-12.md` |
| Sprint 13 | `SPRINT-13.md` |
| Sprint 14 | `SPRINT-14.md` |
| Sprint 15 | `SPRINT-15.md` |
| Sprint 16 | `SPRINT-16.md` |
| Sprint 17 | `SPRINT-17.md` |
| Sprint 18 | `SPRINT-18.md` |
| Sprint 19 | `SPRINT-19.md` |
| Sprint 20 | `SPRINT-20.md` |
