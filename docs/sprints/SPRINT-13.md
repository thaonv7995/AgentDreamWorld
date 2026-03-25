# Sprint 13 – Multi-world Manager, Presets & World Lifecycle UX

## Sprint Metadata

| Field | Value |
| --- | --- |
| Phase | Phase 7 – Multi-world Productization |
| Milestone Gate | Gate H – Multi-world Product Ready |
| Suggested Duration | 2 tuần |
| Primary Validation Signal | User tạo, chọn và quản lý nhiều world với preset khác nhau mà current-world path vẫn rõ và ổn định |
| Source Backlog IDs | `ADW-S13-BA-01`, `ADW-S13-BE-01`, `ADW-S13-FE-01`, `ADW-S13-DO-01` |

## Sprint Goal

Biến multi-world foundation thành product path thật sự usable thay vì chỉ là metadata shell.

## Business Objective

Cho creator và explorer quản lý nhiều world từ UI với preset và lifecycle rõ ràng, không phải thao tác file hoặc env bằng tay.

## Business Value

- Mở world manager như capability thật sau Sprint 12.
- Tạo nền cho world presets và future alternate timeline workflow.
- Giữ single-world happy path còn đơn giản dù hệ thống đã hỗ trợ multi-world.

## In Scope

- Multi-world manager UI/API.
- Create/select/archive world.
- World presets: Balanced, High Chaos, Myth-Heavy.
- Per-world metadata/settings summary.
- Current world switching.

## Out of Scope

- Fast-forward/pacing controls.
- Event Log Viewer / Config Inspector.
- Public community gallery.
- Alternate timeline compare.

## Primary User Stories

- Với vai trò **creator**, tôi muốn tạo nhiều world với preset khác nhau để nuôi nhiều vũ trụ song song.
- Với vai trò **explorer**, tôi muốn chuyển giữa các world mà không mất dấu world hiện tại.
- Với vai trò **maintainer**, tôi muốn archive world cũ để lifecycle dữ liệu rõ ràng hơn.

## Acceptance Criteria

- [ ] User tạo được nhiều world từ UI hoặc product flow chính.
- [ ] Mỗi world có preset và metadata riêng.
- [ ] Switching world không làm lẫn state/feed/config giữa các world.
- [ ] Archive state không phá current-world path.

## Dependencies

- Sprint 12 đã có multi-world metadata model và selector foundation.
- Backend current-world abstraction đủ rõ để chuyển world an toàn.
- Team chốt naming/lifecycle rules cho world states.

## Sprint Task Board

| Task ID | Stream | Summary | Priority | Estimate |
| --- | --- | --- | --- | --- |
| ADW-S13-BA-01 | BA | Chốt UX và lifecycle rules cho multi-world manager | P1 | S |
| ADW-S13-BE-01 | Backend | Implement world manager APIs, presets và state isolation | P1 | XL |
| ADW-S13-FE-01 | Frontend | Implement multi-world manager UI và world creation flow | P1 | L |
| ADW-S13-DO-01 | DevOps | Thiết lập ops checks cho nhiều world active/archive | P2 | M |

## Risks & Control Notes

- Multi-world UI dễ lấn át single-world happy path; phải giữ luồng mặc định thật ngắn.
- Preset semantics phải data-driven, không hard-code lore vào UI.
- Archive/delete lifecycle cần policy rõ để không mất dữ liệu ngoài ý muốn.

## BA Checklist

- [ ] `BA-13.1` Chốt information hierarchy cho world manager.
- [ ] `BA-13.2` Chốt lifecycle states: active, paused, archived.
- [ ] `BA-13.3` Chốt preset semantics và description cho Balanced / High Chaos / Myth-Heavy.
- [ ] `BA-13.4` Chốt acceptance criteria cho create/select/archive flow.
- [ ] `BA-13.5` Review current-world path để tránh UX regression.
- [ ] `BA-13.6` Chuẩn bị handoff rules cho Sprint 14 controls layer.

## Backend Checklist

- [ ] `BE-13.1` Implement create/select/archive APIs cho world lifecycle.
- [ ] `BE-13.2` Persist preset metadata và world settings summary.
- [ ] `BE-13.3` Verify state isolation giữa nhiều world.
- [ ] `BE-13.4` Thêm guards để current world switch không làm hỏng active jobs.
- [ ] `BE-13.5` Tạo fixtures/sample data cho nhiều world preset.
- [ ] `BE-13.6` Document API contract cho manager flow.

## Frontend Checklist

- [ ] `FE-13.1` Implement world manager shell với list/cards rõ ràng.
- [ ] `FE-13.2` Implement create world flow với preset selection.
- [ ] `FE-13.3` Hiển thị world metadata đủ để chọn đúng world.
- [ ] `FE-13.4` Implement current-world switching states/loading/error.
- [ ] `FE-13.5` Feature-gate archive flow để tránh destructive UX mơ hồ.
- [ ] `FE-13.6` Verify empty, single-world, multi-world, archived states.

## DevOps Checklist

- [ ] `DO-13.1` Review storage growth khi nhiều world cùng tồn tại.
- [ ] `DO-13.2` Cập nhật backup naming/retention cho multi-world lifecycle.
- [ ] `DO-13.3` Tạo smoke flow cho create/select/archive world.
- [ ] `DO-13.4` Review monitoring labels theo `world_id`.
- [ ] `DO-13.5` Chuẩn bị restore notes cho archived world path.
- [ ] `DO-13.6` Verify default deployment vẫn dễ vận hành khi chỉ có 1 world.

## Demo & Sign-off

- Demo tạo 2–3 world với preset khác nhau.
- Demo current-world switching và archive flow.
- [ ] Acceptance criteria được review đủ.
- [ ] Current-world path vẫn đơn giản cho user chỉ dùng 1 world.
- [ ] Carry-over items được ghi sang Sprint 14 hoặc `MASTER-BACKLOG.md`.
- Sign-off owners: Project lead + backend lead + frontend lead.
