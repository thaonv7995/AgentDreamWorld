# Sprint 01 – World Model, SQLite Schema, Persistence

## Sprint Metadata

| Field | Value |
| --- | --- |
| Phase | Phase 1 – Engine Foundation |
| Milestone Gate | Gate B – Engine Foundation Ready |
| Suggested Duration | 2 tuần |
| Primary Validation Signal | `GET /worlds/current` trả world summary từ DB thật và persist được sau restart |
| Source Backlog IDs | `ADW-S01-BA-01`, `ADW-S01-BE-01`, `ADW-S01-FE-01`, `ADW-S01-DO-01` |

## Sprint Goal

Chốt domain model và persistence foundation cho V1.

## Business Objective

Xây nền dữ liệu đủ ổn định để toàn bộ simulation, API và UI sau này cùng nói chung một ngôn ngữ domain.

## Business Value

- Khóa vocabulary canon `Region` và `Settlement`.
- Tạo nền cho event pipeline và world summary API.
- Giảm rủi ro churn schema ở các sprint sau.

## In Scope

- SQLite schema V1 — **chỉ 7 core tables** (worlds, regions, locations, civilizations, settlements, events, eras). Defer creatures/religions/cultures/resources sang Sprint 7+.
- Database-per-world naming: `data/world-{name}.db`.
- Migration/init flow với schema version tracking.
- Repository/storage layer cơ bản.
- World seed bootstrap không dùng LLM.
- `GET /worlds/current` trả world summary thật.

## Out of Scope

- Tick orchestration.
- Agent runtime thật.
- Event canonicalization.
- Dream Feed UI thật.

## Primary User Stories

- Với vai trò **backend developer**, tôi muốn có schema rõ ràng để implement persistence mà không phải đoán domain model.
- Với vai trò **frontend developer**, tôi muốn world summary API có contract ổn định để bắt đầu dựng UI.
- Với vai trò **project lead**, tôi muốn vocabulary canon được khóa sớm để tránh drift giữa docs và code.

## Acceptance Criteria

- [ ] App có thể tạo DB và seed world đầu tiên.
- [ ] App restart vẫn đọc lại được world đã seed.
- [ ] `GET /worlds/current` trả về world summary có dữ liệu thật.
- [ ] Schema phản ánh đúng entity canon của V1.
- [ ] Không còn nhầm lẫn top-level entity giữa `Region` và `Settlement`.

## Dependencies

- Sprint 00 hoàn thành scaffold repo.
- Docs `world-model.md` và `database-schema.md` đã được chuẩn hóa.
- Team thống nhất SQLite là default storage V1.

## Sprint Task Board

| Task ID | Stream | Summary | Priority | Estimate |
| --- | --- | --- | --- | --- |
| ADW-S01-BA-01 | BA | Chốt glossary entity và contract `GET /worlds/current` | P1 | S |
| ADW-S01-BE-01 | Backend | Implement schema SQLite V1, migration/init flow và seed world | P1 | L |
| ADW-S01-FE-01 | Frontend | Tạo types world summary và overview shell consume API thật | P2 | S |
| ADW-S01-DO-01 | DevOps | Thêm smoke test cho DB init và chuẩn hóa `data/` path | P2 | S |

## Risks & Control Notes

- Nếu glossary chưa khóa, schema sẽ churn ngay từ sprint tiếp theo.
- Seed world của Sprint 01 phải không phụ thuộc LLM để tránh nhiễu khi test persistence.
- Không mở rộng entity ngoài canon V1 nếu chưa có nhu cầu trực tiếp từ API/engine.

## BA Checklist

- [ ] `BA-01.1` Chốt glossary entity V1 core: World, Region, Location, Civilization, Settlement, Event, Era. Xác nhận **creatures/religions/cultures/resources defer sang V2+**.
- [ ] `BA-01.2` Chốt field-level contract cho `GET /worlds/current` gồm summary blocks bắt buộc và empty-state behavior.
- [ ] `BA-01.3` Chốt definition của seed world: tối thiểu có gì, chưa cần gì, và điều gì bị cấm trong Sprint 01.
- [ ] `BA-01.4` Đối chiếu `world-model.md` và `database-schema.md` để loại bỏ drift trước khi code schema.
- [ ] `BA-01.5` Chốt acceptance criteria cho restart persistence và DB init flow.
- [ ] `BA-01.6` Chuẩn bị checklist handoff cho Sprint 02: event pipeline dựa trên dữ liệu nào từ Sprint 01.

## Backend Checklist

- [ ] `BE-01.1` Implement schema cho `worlds`, `regions`, `locations` theo canon V1.
- [ ] `BE-01.2` Implement schema cho `civilizations`, `settlements` với quan hệ rõ ràng tới region/location.
- [ ] `BE-01.3` Implement schema cho `events`, `eras`. **Không tạo** `religions`, `cultures`, `resources`, `creatures` — defer sang Sprint 7+. Xem [LIMITATIONS.md](../LIMITATIONS.md) §M4.
- [ ] `BE-01.4` Tạo migration/init flow với **schema version tracking** (`schema_version` table) để app boot được DB từ zero state.
- [ ] `BE-01.5` Tạo repository/storage layer tối thiểu cho world summary và seed bootstrap.
- [ ] `BE-01.6` Tạo world seed bootstrap không dùng LLM để test persistence deterministically.
- [ ] `BE-01.7` Expose `GET /worlds/current` bằng dữ liệu thật từ SQLite và verify restart vẫn giữ state.
- [ ] `BE-01.8` **Database-per-world**: SQLite file path theo pattern `data/world-{name}.db`, configurable qua `AI_DREAMS_WORLD_DB`. Xem [LIMITATIONS.md](../LIMITATIONS.md) §M7.1.

## Frontend Checklist

- [ ] `FE-01.1` Tạo types/interfaces cho world summary dựa trên contract đã khóa.
- [ ] `FE-01.2` Tạo world overview shell consume `GET /worlds/current`.
- [ ] `FE-01.3` Implement empty state cho world chưa seed hoặc DB chưa init.
- [ ] `FE-01.4` Tạo summary blocks cho regions, civilizations và settlements.
- [ ] `FE-01.5` Kiểm tra mapping field giữa API response và UI labels để tránh drift thuật ngữ.
- [ ] `FE-01.6` Verify world summary render đúng sau app restart và sau seed bootstrap.

## DevOps Checklist

- [ ] `DO-01.1` Thêm command init/reset DB vào local workflow và docs.
- [ ] `DO-01.2` Định nghĩa nơi lưu SQLite file (`data/`) và policy cho local cleanup.
- [ ] `DO-01.3` Thêm smoke test cho DB init, seed và restart persistence path.
- [ ] `DO-01.4` Thêm CI step validate migrations/schema bootstrap.
- [ ] `DO-01.5` Chuẩn bị sample commands cho developer debug world seed flow.
- [ ] `DO-01.6` Verify repo clone mới có thể đi qua DB init path không cần thao tác ẩn.

## Demo & Sign-off

- Demo seeded world summary từ DB thật.
- Demo app restart vẫn giữ được state.
- [ ] Acceptance criteria được review đủ.
- [ ] Schema canon `Region` và `Settlement` đã khớp docs.
- [ ] Carry-over items được ghi lại sang Sprint 02 hoặc `MASTER-BACKLOG.md`.
- Sign-off owners: Backend lead + BA/project lead.
