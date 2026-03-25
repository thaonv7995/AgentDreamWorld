# Sprint 16 – World Forking, Alternate Timeline Compare & Snapshot Sharing

## Sprint Metadata

| Field | Value |
| --- | --- |
| Phase | Phase 8 – Alternate Timelines & Creator Control |
| Milestone Gate | Gate I – Alternate Timeline Ready |
| Suggested Duration | 2 tuần |
| Primary Validation Signal | User fork được world tại checkpoint, chạy branch và compare với mainline bằng dữ liệu/projection thật |
| Source Backlog IDs | `ADW-S16-BA-01`, `ADW-S16-BE-01`, `ADW-S16-FE-01`, `ADW-S16-DO-01` |

## Sprint Goal

Biến alternate timeline thành product capability thực sự usable.

## Business Objective

Cho creator và explorer xem “what-if” histories một cách rõ ràng, shareable và có provenance thay vì chỉ mô tả bằng text hoặc metadata foundation.

## Business Value

- Đóng vòng alternate timeline vision sau foundation ở Sprint 12.
- Tăng mạnh giá trị exploration và creator experimentation.
- Mở đường cho snapshot sharing, community packages và collaborative scenarios.

## In Scope

- World forking tại year / era / event checkpoint.
- Alternate timeline compare.
- Snapshot sharing.
- Branch provenance/audit metadata.

## Out of Scope

- Public community gallery.
- Multi-user collaborative sessions.
- Per-agent model routing.
- Creator publishing bundle hoàn chỉnh.

## Primary User Stories

- Với vai trò **creator**, tôi muốn fork một world tại thời điểm quan trọng để xem nhánh lịch sử khác.
- Với vai trò **explorer**, tôi muốn compare mainline và branch một cách rõ ràng.
- Với vai trò **maintainer**, tôi muốn provenance của branch/snapshot đủ rõ để trace về source.

## Acceptance Criteria

- [ ] User fork được world tại checkpoint hợp lệ.
- [ ] Branch chạy tiếp được mà không làm hỏng mainline.
- [ ] Compare view hiển thị divergence summary readable.
- [ ] Snapshot sharing giữ provenance/version metadata rõ ràng.

## Dependencies

- Sprint 15 creator control và arc/highlight layer đã có.
- Sprint 12 snapshot/fork foundation ổn định ở tầng model/storage.
- Multi-world manager từ Sprint 13 đủ trưởng thành để chứa branch worlds.

## Sprint Task Board

| Task ID | Stream | Summary | Priority | Estimate |
| --- | --- | --- | --- | --- |
| ADW-S16-BA-01 | BA | Chốt UX fork/compare và provenance rules cho snapshots | P1 | S |
| ADW-S16-BE-01 | Backend | Implement world forking, branch compare và snapshot sharing | P1 | XL |
| ADW-S16-FE-01 | Frontend | Implement alternate timeline UX và snapshot share flow | P1 | XL |
| ADW-S16-DO-01 | DevOps | Tạo storage/recovery policy cho forks và snapshots | P2 | M |

## Risks & Control Notes

- Fork path có thể phình storage rất nhanh nếu retention mơ hồ.
- Compare UX dễ biến thành bảng số liệu khó đọc; phải ưu tiên divergence summary rõ.
- Snapshot sharing phải đủ nhẹ để dùng nội bộ trước khi mở community gallery.

## BA Checklist

- [ ] `BA-16.1` Chốt fork checkpoints: year, era, event.
- [ ] `BA-16.2` Chốt compare semantics cho divergence summary.
- [ ] `BA-16.3` Chốt provenance/version fields cho branch và snapshot.
- [ ] `BA-16.4` Chốt acceptance criteria của Gate I.
- [ ] `BA-16.5` Chốt UX boundary giữa branch nội bộ và shareable snapshot.
- [ ] `BA-16.6` Chuẩn bị handoff cho runtime flexibility và creator export phases.

## Backend Checklist

- [ ] `BE-16.1` Implement fork orchestration từ checkpoint hợp lệ.
- [ ] `BE-16.2` Ensure branch/mainline isolation ở data/runtime layers.
- [ ] `BE-16.3` Implement branch compare projection.
- [ ] `BE-16.4` Implement snapshot artifact generation với provenance metadata.
- [ ] `BE-16.5` Add tests cho branch integrity và compare correctness.
- [ ] `BE-16.6` Document recovery/migration path cho forked worlds.

## Frontend Checklist

- [ ] `FE-16.1` Implement fork flow từ timeline/checkpoint surfaces.
- [ ] `FE-16.2` Implement branch list/navigation trong multi-world UX.
- [ ] `FE-16.3` Implement compare screen hoặc divergence summary panels.
- [ ] `FE-16.4` Implement snapshot share/export states.
- [ ] `FE-16.5` Giữ mainline path rõ ràng, tránh user lẫn branch với source world.
- [ ] `FE-16.6` Verify empty/loading/error states cho fork/compare/share.

## DevOps Checklist

- [ ] `DO-16.1` Chốt retention và cleanup policy cho branches/snapshots.
- [ ] `DO-16.2` Tạo drill test cho restore một branch hoặc snapshot.
- [ ] `DO-16.3` Theo dõi storage growth và clone/fork latency.
- [ ] `DO-16.4` Verify provenance logs/audit trail khi fork world.
- [ ] `DO-16.5` Chuẩn bị demo world có divergence rõ ràng.
- [ ] `DO-16.6` Review cost impact khi chạy nhiều branch song song.

## Demo & Sign-off

- Demo fork một world tại checkpoint rõ ràng.
- Demo compare mainline và branch.
- [ ] Acceptance criteria được review đủ.
- [ ] Gate I có bằng chứng alternate timeline usable end-to-end.
- [ ] Carry-over items được ghi sang Sprint 17 hoặc `MASTER-BACKLOG.md`.
- Sign-off owners: Project lead + backend lead + DevOps lead.
