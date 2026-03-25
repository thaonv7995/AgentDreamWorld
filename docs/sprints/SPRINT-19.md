# Sprint 19 – Community Worlds, Package Export/Import & Shared Gallery

## Sprint Metadata

| Field | Value |
| --- | --- |
| Phase | Phase 10 – Community & Collaboration |
| Milestone Gate | Gate K – Community Vision Ready |
| Suggested Duration | 2 tuần |
| Primary Validation Signal | User export/import được world packages và browse được shared gallery với provenance/version metadata rõ ràng |
| Source Backlog IDs | `ADW-S19-BA-01`, `ADW-S19-BE-01`, `ADW-S19-FE-01`, `ADW-S19-DO-01` |

## Sprint Goal

Biến world thành asset có thể chia sẻ, remix và khám phá như một ecosystem.

## Business Objective

Cho cộng đồng export/import world, xem gallery chung và tin tưởng provenance/package compatibility trước khi collaborative mode được mở.

## Business Value

- Chạm trực tiếp phần Community Worlds trong vision docs.
- Tăng value của mỗi world vì có thể được tái sử dụng ngoài máy tạo ra nó.
- Mở nền trust/moderation trước khi có shared live sessions.

## In Scope

- World package spec.
- Export/import world packages.
- Shared gallery.
- Provenance/version metadata.
- Basic moderation flags.

## Out of Scope

- Collaborative realtime sessions.
- Shared God Mode live conflicts.
- Marketplace hoặc monetization layer.
- Open-ended social feed.

## Primary User Stories

- Với vai trò **creator**, tôi muốn export world để người khác import và chạy tiếp.
- Với vai trò **explorer**, tôi muốn browse gallery và biết package đến từ đâu.
- Với vai trò **maintainer**, tôi muốn compatibility và provenance rules đủ rõ để support được shared artifacts.

## Acceptance Criteria

- [ ] Package export/import usable end-to-end.
- [ ] Gallery hiển thị metadata/provenance rõ ràng.
- [ ] Package versioning chặn được import drift cơ bản.
- [ ] Shared worlds không yêu cầu collaborative mode mới có giá trị.

## Dependencies

- Sprint 18 creator bundles và artifact metadata đã chốt.
- Sprint 16 snapshots/branches có provenance đủ mạnh để tái sử dụng.
- Storage/publish path đủ trưởng thành cho world packages.

## Sprint Task Board

| Task ID | Stream | Summary | Priority | Estimate |
| --- | --- | --- | --- | --- |
| ADW-S19-BA-01 | BA | Chốt world package spec, provenance fields và gallery UX | P1 | S |
| ADW-S19-BE-01 | Backend | Implement package export/import, versioning và shared gallery APIs | P1 | XL |
| ADW-S19-FE-01 | Frontend | Implement community gallery và import/export flows | P1 | XL |
| ADW-S19-DO-01 | DevOps | Tạo moderation/runbook và package compatibility checks | P2 | M |

## Risks & Control Notes

- Package import từ nguồn lạ là trust boundary rõ ràng; provenance và versioning không được xem nhẹ.
- Gallery UX dễ trở thành dump metadata nếu không có curation/filter tốt.
- Shared package support sẽ làm tăng support burden nếu format không ổn định.

## BA Checklist

- [ ] `BA-19.1` Chốt world package fields bắt buộc.
- [ ] `BA-19.2` Chốt provenance/moderation metadata tối thiểu.
- [ ] `BA-19.3` Chốt gallery taxonomy và filters cần có.
- [ ] `BA-19.4` Chốt acceptance criteria cho import/export flows.
- [ ] `BA-19.5` Review compatibility policy giữa package versions.
- [ ] `BA-19.6` Chuẩn bị handoff sang collaborative sessions ở Sprint 20.

## Backend Checklist

- [ ] `BE-19.1` Implement world package serializer/deserializer.
- [ ] `BE-19.2` Implement package import validation/version checks.
- [ ] `BE-19.3` Expose gallery APIs với provenance metadata.
- [ ] `BE-19.4` Add moderation/status fields trong package/gallery model.
- [ ] `BE-19.5` Add tests cho round-trip export/import.
- [ ] `BE-19.6` Document package contract cho future community tooling.

## Frontend Checklist

- [ ] `FE-19.1` Implement export/import entry points cho world packages.
- [ ] `FE-19.2` Implement shared gallery browse/filter views.
- [ ] `FE-19.3` Hiển thị provenance, version và moderation/status badges rõ ràng.
- [ ] `FE-19.4` Implement import validation/error UX.
- [ ] `FE-19.5` Cross-link gallery items với local world manager khi import xong.
- [ ] `FE-19.6` Verify empty/loading/error states cho gallery và import flow.

## DevOps Checklist

- [ ] `DO-19.1` Chốt moderation/runbook cho shared packages.
- [ ] `DO-19.2` Verify compatibility checks hoạt động ở import path.
- [ ] `DO-19.3` Review storage/caching strategy cho gallery artifacts.
- [ ] `DO-19.4` Tạo smoke tests cho package round-trip.
- [ ] `DO-19.5` Chuẩn bị rollback/restore notes cho failed imports.
- [ ] `DO-19.6` Review trust boundary và abuse scenarios của package sharing.

## Demo & Sign-off

- Demo export một world package và import lại thành công.
- Demo shared gallery với provenance/version metadata.
- [ ] Acceptance criteria được review đủ.
- [ ] Shared packages usable mà chưa cần collaborative realtime.
- [ ] Carry-over items được ghi sang Sprint 20 hoặc `MASTER-BACKLOG.md`.
- Sign-off owners: Project lead + backend lead + DevOps lead.
