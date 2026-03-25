# Sprint 12 – Multi-world Foundation & Project Ops

## Sprint Metadata

| Field | Value |
| --- | --- |
| Phase | Phase 6 – Platform Expansion |
| Milestone Gate | Gate G – Platform Expansion Ready |
| Suggested Duration | 2 tuần |
| Primary Validation Signal | Multi-world foundation vào được metadata/model/ops layer mà current-world UX vẫn nguyên vẹn |
| Source Backlog IDs | `ADW-S12-BA-01`, `ADW-S12-BE-01`, `ADW-S12-FE-01`, `ADW-S12-DO-01` |

## Sprint Goal

Mở nền cho multi-world mà không phá trải nghiệm current-world.

## Business Objective

Chuẩn bị cấu trúc dữ liệu và vận hành cho tương lai multi-world, alternate timeline và world fork, nhưng vẫn giữ luồng hiện tại đơn giản.

## Business Value

- Mở đường cho Phase 7+ và roadmap dài hạn.
- Giảm rủi ro rework lớn khi muốn hỗ trợ nhiều world.
- Tạo nền vận hành rõ hơn cho lifecycle world data.

## In Scope

- Multi-world metadata model.
- Snapshot/fork foundation.
- World gallery metadata.
- Project ops runbook baseline.

## Out of Scope

- Shared worlds gallery hoàn chỉnh.
- Collaborative storytelling.
- Full alternate timeline UX.
- Marketplace/community layer.

## Primary User Stories

- Với vai trò **maintainer**, tôi muốn hệ thống không assume chỉ có một world duy nhất mãi mãi.
- Với vai trò **user nâng cao**, tôi muốn có nền cho việc giữ nhiều world hoặc fork world sau này.
- Với vai trò **project lead**, tôi muốn roadmap multi-world có thể bắt đầu mà không phá current-world UX.

## Acceptance Criteria

- [ ] Data model không còn assume duy nhất một world forever.
- [ ] Current-world UX vẫn hoạt động.
- [ ] Có nền để làm alternate timeline/fork sau này.
- [ ] Ops runbook mô tả được lifecycle snapshot/fork cơ bản.

## Dependencies

- Sprint 11 đã có baseline observability và ops thinking.
- Backend model đủ trưởng thành để tách current world khỏi multi-world metadata.
- Team thống nhất boundary giữa “foundation” và “full multi-world product”.

## Sprint Task Board

| Task ID | Stream | Summary | Priority | Estimate |
| --- | --- | --- | --- | --- |
| ADW-S12-BA-01 | BA | Chốt use cases multi-world, fork và snapshot metadata | P1 | S |
| ADW-S12-BE-01 | Backend | Implement multi-world metadata model và snapshot/fork foundation | P1 | XL |
| ADW-S12-FE-01 | Frontend | Tạo world selector/world list shell | P2 | M |
| ADW-S12-DO-01 | DevOps | Tạo ops runbook và workflows backup/restore multi-world | P1 | M |

## Risks & Control Notes

- Multi-world foundation dễ làm rò rỉ complexity sang current-world UX; phải giữ user path hiện tại đơn giản.
- Migration/backward compatibility phải rõ từ đầu để không làm vỡ current-world endpoints.
- Sprint này chỉ xây foundation và ops rules, chưa mở full alternate timeline product.

## BA Checklist

- [ ] `BA-12.1` Chốt use cases multi-world, snapshot và world fork.
- [ ] `BA-12.2` Chốt rule snapshot/fork metadata và boundary giữa foundation với full product.
- [ ] `BA-12.3` Chốt acceptance criteria cho world gallery metadata.
- [ ] `BA-12.4` Review impact với current-world UX.
- [ ] `BA-12.5` Chốt navigation assumptions cho world selector ở mức tối thiểu.
- [ ] `BA-12.6` Chuẩn bị handoff notes cho roadmap sau Sprint 12.

## Backend Checklist

- [ ] `BE-12.1` Implement multi-world metadata model không phá current-world data path.
- [ ] `BE-12.2` Implement world selector/current world abstraction ở backend.
- [ ] `BE-12.3` Implement snapshot/fork foundation ở mức metadata và storage hooks.
- [ ] `BE-12.4` Ensure backward compatibility với current-world endpoints hoặc tạo migration path rõ.
- [ ] `BE-12.5` Verify current-world assumptions không còn hard-coded trong core flows.
- [ ] `BE-12.6` Tạo sample data hoặc fixtures cho nhiều world metadata để frontend/devops test.

## Frontend Checklist

- [ ] `FE-12.1` Tạo world selector hoặc world list shell ở mức foundation.
- [ ] `FE-12.2` Hiển thị basic world gallery metadata.
- [ ] `FE-12.3` Giữ current-world flow đơn giản, không làm user path rối.
- [ ] `FE-12.4` Chuẩn bị UI contract cho future alternate timelines.
- [ ] `FE-12.5` Verify current-world path không regression khi multi-world metadata tồn tại.
- [ ] `FE-12.6` Verify selector/gallery states cho empty, single-world và multi-world cases.

## DevOps Checklist

- [ ] `DO-12.1` Tạo backup/restore workflow cho nhiều world.
- [ ] `DO-12.2` Tạo ops runbook cho snapshot/fork lifecycle.
- [ ] `DO-12.3` Review storage lifecycle và cleanup policy cho world growth.
- [ ] `DO-12.4` Cập nhật monitoring cho multi-world growth.
- [ ] `DO-12.5` Chạy drill test cho snapshot, restore hoặc metadata recovery path tối thiểu.
- [ ] `DO-12.6` Verify world growth policy không làm current deployment path phức tạp quá mức.

## Demo & Sign-off

- Demo hệ thống có thể chứa nhiều world metadata.
- Demo current-world path vẫn chạy bình thường.
- [ ] Acceptance criteria được review đủ.
- [ ] Current-world UX không bị regression bởi metadata multi-world.
- [ ] Carry-over items được ghi lại vào backlog vận hành tiếp theo.
- Sign-off owners: Project lead + backend lead + DevOps lead.
