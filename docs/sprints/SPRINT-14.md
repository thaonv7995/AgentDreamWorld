# Sprint 14 – Pace Control, Fast-forward, Event Log Viewer & Config Inspector

## Sprint Metadata

| Field | Value |
| --- | --- |
| Phase | Phase 7 – Multi-world Productization |
| Milestone Gate | Gate H – Multi-world Product Ready |
| Suggested Duration | 2 tuần |
| Primary Validation Signal | Creator/operator có thể tăng giảm tốc, fast-forward và inspect từng world bằng dữ liệu thật |
| Source Backlog IDs | `ADW-S14-BA-01`, `ADW-S14-BE-01`, `ADW-S14-FE-01`, `ADW-S14-DO-01` |

## Sprint Goal

Làm cho multi-world product có đủ control và inspection tooling để vận hành thực tế.

## Business Objective

Cho creator và maintainer nhìn rõ một world đang chạy gì, cấu hình ra sao, và có thể đổi tốc độ mà không cần thao tác thủ công dưới backend.

## Business Value

- Biến multi-world từ “có thể tồn tại” thành “có thể điều khiển và debug”.
- Giảm friction cho world farming, content harvesting và tuning.
- Khóa Gate H bằng một product slice hoàn chỉnh hơn cho multi-world.

## In Scope

- Pace control: Slow / Normal / Fast.
- Fast-forward: +50 năm, +100 năm, +1 era.
- Event Log Viewer.
- Config Inspector.
- Per-world runtime status.

## Out of Scope

- Advanced God Mode.
- Story Arc Highlighter.
- World forking / compare UX.
- Community gallery.

## Primary User Stories

- Với vai trò **creator**, tôi muốn tăng tốc một world để farm lịch sử nhanh hơn.
- Với vai trò **operator**, tôi muốn inspect log/config của từng world mà không chạm DB trực tiếp.
- Với vai trò **maintainer**, tôi muốn debug tại sao một world chạy khác world khác.

## Acceptance Criteria

- [ ] User đổi được pace của một world.
- [ ] Fast-forward chạy được theo contract đã chốt.
- [ ] Event Log Viewer hiển thị raw/canonical events theo filter.
- [ ] Config Inspector phản ánh đúng settings thật của world/runtime.

## Dependencies

- Sprint 13 world manager và lifecycle UX đã ổn.
- Tick runner hỗ trợ state transition an toàn khi đổi pace/fast-forward.
- Observability/logging từ Sprint 02–03 và Sprint 11 đã đủ dữ liệu.

## Sprint Task Board

| Task ID | Stream | Summary | Priority | Estimate |
| --- | --- | --- | --- | --- |
| ADW-S14-BA-01 | BA | Chốt control semantics cho pace/fast-forward và inspector UX | P1 | S |
| ADW-S14-BE-01 | Backend | Implement pace control, fast-forward, log/config projections | P1 | XL |
| ADW-S14-FE-01 | Frontend | Implement pace controls, Event Log Viewer, Config Inspector | P1 | XL |
| ADW-S14-DO-01 | DevOps | Tạo verification flow cho fast-forward, pacing và inspection metrics | P2 | M |

## Risks & Control Notes

- Fast-forward dễ làm spike cost hoặc phá coherence nếu reuse path sai.
- Event Log Viewer phải scale theo filters/paging, không dump log vô hạn.
- Config Inspector không được leak quá nhiều complexity cho user path bình thường.

## BA Checklist

- [ ] `BA-14.1` Chốt semantics cho Slow / Normal / Fast.
- [ ] `BA-14.2` Chốt semantics cho +50 / +100 / +1 era.
- [ ] `BA-14.3` Chốt information hierarchy của Event Log Viewer.
- [ ] `BA-14.4` Chốt nhóm config nào được expose trong Config Inspector.
- [ ] `BA-14.5` Review acceptance criteria cho Gate H.
- [ ] `BA-14.6` Chuẩn bị handoff notes cho creator control ở Sprint 15.

## Backend Checklist

- [ ] `BE-14.1` Implement per-world pace control state.
- [ ] `BE-14.2` Implement fast-forward orchestration theo checkpoint an toàn.
- [ ] `BE-14.3` Expose Event Log Viewer projections với paging/filter contract.
- [ ] `BE-14.4` Expose Config Inspector payload cho world/runtime settings.
- [ ] `BE-14.5` Verify fast-forward không phá canonical/raw invariants.
- [ ] `BE-14.6` Add tests cho pace switching, fast-forward và inspector contracts.

## Frontend Checklist

- [ ] `FE-14.1` Implement pace controls trong world controls area.
- [ ] `FE-14.2` Implement fast-forward UI states và confirmations cần thiết.
- [ ] `FE-14.3` Implement Event Log Viewer với filters cơ bản.
- [ ] `FE-14.4` Implement Config Inspector cho debug/admin path.
- [ ] `FE-14.5` Giữ regular viewer path không bị nhiễu bởi tooling nâng cao.
- [ ] `FE-14.6` Verify empty/error/loading states cho log/config panels.

## DevOps Checklist

- [ ] `DO-14.1` Tạo soak run cho nhiều pace modes.
- [ ] `DO-14.2` Đo cost/time delta giữa Normal và fast-forward paths.
- [ ] `DO-14.3` Verify logs/metrics phản ánh đúng state changes.
- [ ] `DO-14.4` Chuẩn bị recovery notes nếu fast-forward bị abort giữa chừng.
- [ ] `DO-14.5` Review perf impact của log viewer queries.
- [ ] `DO-14.6` Chốt demo script cho Gate H.

## Demo & Sign-off

- Demo đổi pace của nhiều world.
- Demo fast-forward và Event Log Viewer/Config Inspector dùng dữ liệu thật.
- [ ] Acceptance criteria được review đủ.
- [ ] Gate H có đủ bằng chứng để close ở mức product slice, không chỉ infra foundation.
- [ ] Carry-over items được ghi sang Sprint 15 hoặc `MASTER-BACKLOG.md`.
- Sign-off owners: Project lead + backend lead + DevOps lead.
