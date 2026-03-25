# Sprint 02 – Event Pipeline, Tick Runner, Guardian/Historian

## Sprint Metadata

| Field | Value |
| --- | --- |
| Phase | Phase 1 – Engine Foundation |
| Milestone Gate | Gate B – Engine Foundation Ready |
| Suggested Duration | 2 tuần |
| Primary Validation Signal | Manual tick sinh event hợp lệ, qua Guardian/Historian và commit được vào world state |
| Source Backlog IDs | `ADW-S02-BA-01`, `ADW-S02-BE-01`, `ADW-S02-FE-01`, `ADW-S02-DO-01` |

## Sprint Goal

Có simulation loop tối thiểu chạy end-to-end bằng mock logic.

## Business Objective

Thiết lập “xương sống” của Dream Engine: proposal, validation, canonicalization và commit world state.

## Business Value

- Chứng minh core architecture hoạt động thật.
- Tạo đường sống cho mọi feature simulation về sau.
- Tách rõ imagination layer và canonical layer ngay từ đầu.

## In Scope

- `EventProposal`.
- Append-only event log.
- Tick orchestrator.
- Mock `AgentModel`.
- Guardian validation baseline.
- Historian canonicalization baseline.
- `POST /worlds/current/tick`.

## Out of Scope

- 3 creative agents thật.
- Genesis mode hoàn chỉnh.
- UI Dream Feed hoàn chỉnh.
- Live LLM provider production quality.

## Primary User Stories

- Với vai trò **developer**, tôi muốn trigger một tick thủ công để kiểm tra simulation pipeline end-to-end.
- Với vai trò **runtime owner**, tôi muốn Guardian và Historian có baseline rõ để bảo vệ canonical world state.
- Với vai trò **PM/lead**, tôi muốn thấy bằng chứng kiến trúc event-sourced có thể chạy thật, không chỉ nằm trên docs.

## Acceptance Criteria

- [ ] Manual tick tạo ra event hợp lệ.
- [ ] Guardian reject được event sai ID hoặc sai progression cơ bản.
- [ ] Historian đánh dấu được canonical event.
- [ ] Raw events và canonical events được phân biệt rõ.
- [ ] Event log append-only hoạt động đúng.

## Dependencies

- Sprint 01 đã có schema và storage foundation.
- Contract `event-model.md` đã ổn định.
- Mock model path được thống nhất để giảm phụ thuộc LLM thật.

## Sprint Task Board

| Task ID | Stream | Summary | Priority | Estimate |
| --- | --- | --- | --- | --- |
| ADW-S02-BA-01 | BA | Chốt event lifecycle, raw/canonical rules và contract tick endpoint | P1 | S |
| ADW-S02-BE-01 | Backend | Implement event pipeline, append-only log, tick orchestrator và validation flow | P1 | L |
| ADW-S02-FE-01 | Frontend | Tạo debug tick trigger và event list shell cho demo/test | P2 | S |
| ADW-S02-DO-01 | DevOps | Thêm logs, env flags và smoke test cho tick lifecycle | P2 | S |

## Risks & Control Notes

- Dễ nhầm raw event với canonical event nếu không tách rõ trạng thái và ownership.
- Không gắn prompt/provider logic thật quá sớm vào tick runner; mock path phải đứng được một mình.
- Tick endpoint chỉ phục vụ dev/debug ở sprint này, chưa phải public control surface hoàn chỉnh.

## BA Checklist

- [ ] `BA-02.1` Chốt event lifecycle chi tiết: proposal -> validation -> canonical -> projection -> persistence.
- [ ] `BA-02.2` Chốt raw vs canonical acceptance rules, bao gồm ai là owner của mỗi trạng thái.
- [ ] `BA-02.3` Chốt contract cho `POST /worlds/current/tick`, gồm request, response và error cases.
- [ ] `BA-02.4` Chốt tiêu chí reject cơ bản của Guardian và tiêu chí promote của Historian.
- [ ] `BA-02.5` Chuẩn bị sample scenarios cho valid tick, rejected tick và canonicalized tick.
- [ ] `BA-02.6` Review docs event-model để đảm bảo runtime team và frontend team đọc cùng một pipeline.

## Backend Checklist

- [ ] `BE-02.1` Implement `EventProposal` model và relation với world state hiện tại.
- [ ] `BE-02.2` Implement append-only event persistence cho raw events và canonical events.
- [ ] `BE-02.3` Implement tick orchestrator điều phối generate -> validate -> canonicalize -> commit.
- [ ] `BE-02.4` Implement mock `AgentModel` để tick chạy không phụ thuộc provider thật.
- [ ] `BE-02.5` Implement Guardian rules baseline cho ID, chronology và progression checks.
- [ ] `BE-02.6` Implement Historian canonicalization baseline và canonical marker.
- [ ] `BE-02.7` Expose `POST /worlds/current/tick` và verify happy path lẫn reject path.

## Frontend Checklist

- [ ] `FE-02.1` Tạo debug action/panel để trigger manual tick từ UI.
- [ ] `FE-02.2` Tạo event list shell đọc canonical events sau mỗi tick.
- [ ] `FE-02.3` Hiển thị trạng thái tick success, reject, failure và loading.
- [ ] `FE-02.4` Phân biệt hiển thị raw debug info với canonical event list nếu cần cho dev mode.
- [ ] `FE-02.5` Chuẩn bị event card model cho Dream Feed sprint sau.
- [ ] `FE-02.6` Verify manual tick cập nhật UI mà không cần reload thủ công toàn bộ app.

## DevOps Checklist

- [ ] `DO-02.1` Thêm structured logs cho tick lifecycle từ proposal tới commit/reject.
- [ ] `DO-02.2` Thêm env flags cho mock/live model mode và default rõ cho local dev.
- [ ] `DO-02.3` Thêm smoke test cho manual tick happy path.
- [ ] `DO-02.4` Thêm smoke test cho reject/failure path tối thiểu.
- [ ] `DO-02.5` Thiết lập error logging tối thiểu cho orchestration và DB write failures.
- [ ] `DO-02.6` Chuẩn bị commands reset/reseed world để lặp lại demo tick flow ổn định.

## Demo & Sign-off

- Demo trigger 1 tick và thấy event được ghi xuống DB.
- Demo Guardian reject path và canonical path.
- [ ] Acceptance criteria được review đủ.
- [ ] Raw event và canonical event đã có ranh giới rõ trong docs/code contract.
- [ ] Carry-over items được ghi lại sang Sprint 03 hoặc `MASTER-BACKLOG.md`.
- Sign-off owners: Backend lead + runtime owner + project lead.
