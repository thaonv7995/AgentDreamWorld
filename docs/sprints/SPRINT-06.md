# Sprint 06 – Export, Single-Binary Mode, MVP Hardening

## Sprint Metadata

| Field | Value |
| --- | --- |
| Phase | Phase 3 – MVP Release Candidate |
| Milestone Gate | Gate D – MVP Release Candidate |
| Suggested Duration | 2 tuần |
| Primary Validation Signal | MVP đi end-to-end từ world generation tới export trong single-binary mode, không còn blocker chính |
| Source Backlog IDs | `ADW-S06-BA-01`, `ADW-S06-BE-01`, `ADW-S06-FE-01`, `ADW-S06-DO-01` |

## Sprint Goal

Đưa V1 tới mức release candidate đúng Definition of Done.

## Business Objective

Chốt MVP thành một gói có thể demo và dùng được như sản phẩm nền đầu tiên: world generation, exploration, export và local delivery path.

## Business Value

- Đạt Gate D của dự án.
- Tạo mốc rõ ràng giữa MVP và post-MVP.
- Tạo khả năng xuất content đúng với value proposition đã mô tả trong PRD.

## In Scope

- Wiki export.
- Annals export.
- Single-binary mode.
- MVP hardening pass.
- QA theo DoD của `MVP-SPEC.md`.

## Out of Scope

- Culture/Myth/Ecology/Economy/Chaos.
- Map/graph visualization.
- Advanced infra profile.
- Multi-world support.

## Primary User Stories

- Với vai trò **content creator**, tôi muốn export wiki/annals để tái sử dụng world thành content.
- Với vai trò **user local**, tôi muốn chạy app theo mode đơn giản nhất có thể.
- Với vai trò **project lead**, tôi muốn có MVP release candidate đo được theo DoD thay vì “gần xong”.

## Acceptance Criteria

- [ ] Đạt DoD của `MVP-SPEC.md`.
- [ ] Export files readable và có cấu trúc rõ.
- [ ] Single-binary mode chạy được.
- [ ] MVP path không còn blocker bug.
- [ ] Demo end-to-end đi qua world generation → observation → export.

## Dependencies

- Sprint 05 đã có timeline và control path.
- Summary/data model ổn định đủ để export.
- Frontend build có thể được backend serve.

## Sprint Task Board

| Task ID | Stream | Summary | Priority | Estimate |
| --- | --- | --- | --- | --- |
| ADW-S06-BA-01 | BA | Chốt format export và sign-off MVP DoD | P1 | S |
| ADW-S06-BE-01 | Backend | Implement wiki/annals export và backend serve static frontend | P1 | L |
| ADW-S06-FE-01 | Frontend | Implement export UI và polish MVP path | P1 | M |
| ADW-S06-DO-01 | DevOps | Tạo release pipeline single-binary và smoke export flow | P1 | M |

## Risks & Control Notes

- Gate D chỉ pass khi đạt DoD rõ ràng; không dùng cảm giác “gần xong” để chốt MVP.
- Export output phải usable cho người đọc thật, không chỉ đúng JSON/file structure.
- Hardening chỉ tập trung vào blocker path của MVP, không mở cửa cho post-MVP scope.

## BA Checklist

- [ ] `BA-06.1` Chốt format output cho wiki export: structure, headings và minimum sections.
- [ ] `BA-06.2` Chốt format output cho annals export và tiêu chí readability.
- [ ] `BA-06.3` Review MVP DoD checklist và map từng mục vào owner stream.
- [ ] `BA-06.4` Chốt rõ những gì bắt buộc và những gì bị cắt khỏi MVP.
- [ ] `BA-06.5` Chuẩn bị demo script end-to-end cho Gate D.
- [ ] `BA-06.6` Chuẩn bị sign-off pack để tránh tranh cãi “xong/chưa xong” ở cuối sprint.

## Backend Checklist

- [ ] `BE-06.1` Implement `/export/wiki` với serializer/output path ổn định.
- [ ] `BE-06.2` Implement `/export/annals` với structure phù hợp content reuse.
- [ ] `BE-06.3` Implement backend serve static frontend cho single-binary mode.
- [ ] `BE-06.4` Cleanup config, startup path và error handling của MVP.
- [ ] `BE-06.5` Fix blocker bugs trên world generation, observer flow và export path.
- [ ] `BE-06.6` Verify MVP DoD end-to-end từ backend perspective bằng smoke path có lặp lại.

## Frontend Checklist

- [ ] `FE-06.1` Implement export actions UI trong flow người dùng tự nhiên.
- [ ] `FE-06.2` Implement export progress, success và error states.
- [ ] `FE-06.3` Polish Dream Feed, Timeline và Overview cho MVP path.
- [ ] `FE-06.4` Remove obvious placeholder hoặc mock-only UX còn sót.
- [ ] `FE-06.5` Verify export flow không phá observer flow hiện có.
- [ ] `FE-06.6` Verify MVP demo path từ UI có thể đi xuyên suốt mà không cần debug controls.

## DevOps Checklist

- [ ] `DO-06.1` Build release pipeline cho single-binary mode.
- [ ] `DO-06.2` Tạo packaging và artifact naming convention rõ ràng.
- [ ] `DO-06.3` Thêm smoke test cho export flow và startup single-binary.
- [ ] `DO-06.4` Chuẩn bị release notes, install notes và demo checklist.
- [ ] `DO-06.5` Verify artifact chạy được trên local delivery path mục tiêu.
- [ ] `DO-06.6` Ghi lại rollback hoặc fallback path nếu Gate D fail ở phút cuối.

## Demo & Sign-off

- Demo full MVP path từ world generation tới export wiki/annals.
- [ ] Acceptance criteria được review đủ.
- [ ] DoD của `MVP-SPEC.md` được check lại từng mục.
- [ ] Carry-over items được ghi lại sang Sprint 07 hoặc `MASTER-BACKLOG.md`.
- Sign-off owners: Project lead + BA + technical leads.
