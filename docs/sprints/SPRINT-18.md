# Sprint 18 – Myths Export, Highlight Packs & Creator Publishing Pipeline

## Sprint Metadata

| Field | Value |
| --- | --- |
| Phase | Phase 9 – Runtime Flexibility & Creator Publishing |
| Milestone Gate | Gate J – Creator Runtime Ready |
| Suggested Duration | 2 tuần |
| Primary Validation Signal | Creator xuất được artifact packs hoàn chỉnh gồm myths/arcs/highlights mà không cần chắp vá thủ công từ nhiều màn hình |
| Source Backlog IDs | `ADW-S18-BA-01`, `ADW-S18-BE-01`, `ADW-S18-FE-01`, `ADW-S18-DO-01` |

## Sprint Goal

Biến world output thành creator-ready publishing pipeline thay vì chỉ là các export rời rạc.

## Business Objective

Cho writers, video creators và worldbuilders lấy một world hoặc branch và xuất ra một bộ tài liệu/artifact đủ để làm blog, video hoặc lore package.

## Business Value

- Chạm đúng use case content creator trong vision docs.
- Nâng export từ “có file” thành “có bộ asset usable”.
- Gắn story arcs, myths và highlights vào một pipeline xuất bản rõ ràng.

## In Scope

- Myths & Legends export.
- Story arc export packs.
- Highlight reel manifests.
- Unified creator bundle.
- Optional remote artifact path.

## Out of Scope

- Public community gallery.
- Collaborative viewing.
- Fully automated video rendering pipeline.
- Moderation workflow cho shared artifacts.

## Primary User Stories

- Với vai trò **content creator**, tôi muốn xuất bộ lore pack hoàn chỉnh cho một world.
- Với vai trò **writer**, tôi muốn myths, annals, arcs và highlights link với nhau.
- Với vai trò **maintainer**, tôi muốn artifact bundle có naming/versioning rõ ràng.

## Acceptance Criteria

- [ ] Creator bundle gồm wiki, annals, myths, arcs, highlights.
- [ ] Bundle readable và truy vết được về source world/branch.
- [ ] Artifact naming/versioning rõ ràng.
- [ ] UI export flow không yêu cầu user ghép tay nhiều export rời.

## Dependencies

- Sprint 15–16 đã có story arcs và snapshots/branches.
- Export foundations từ Sprint 6 và mythology layer từ Sprint 7–10 đã usable.
- Runtime profile/export storage path đủ ổn để xuất artifact lớn hơn.

## Sprint Task Board

| Task ID | Stream | Summary | Priority | Estimate |
| --- | --- | --- | --- | --- |
| ADW-S18-BA-01 | BA | Chốt creator pack format cho myths/arcs/highlights | P1 | S |
| ADW-S18-BE-01 | Backend | Implement myths export, highlight manifests và publishing bundles | P1 | XL |
| ADW-S18-FE-01 | Frontend | Implement creator export UI và artifact browsing flow | P1 | L |
| ADW-S18-DO-01 | DevOps | Thiết lập artifact retention và publish/storage workflow | P2 | M |

## Risks & Control Notes

- Creator bundle dễ biến thành dump file khó dùng nếu structure kém.
- Highlight manifests phải gắn rõ source events để tránh hallucinated packaging.
- Optional remote artifact path không được trở thành hard dependency.

## BA Checklist

- [ ] `BA-18.1` Chốt structure của creator bundle.
- [ ] `BA-18.2` Chốt output contract cho myths/arcs/highlights.
- [ ] `BA-18.3` Chốt naming/version/provenance rules cho artifacts.
- [ ] `BA-18.4` Chốt acceptance criteria cho Gate J creator side.
- [ ] `BA-18.5` Review optional remote artifact path và non-goals.
- [ ] `BA-18.6` Chuẩn bị handoff sang community packaging ở Sprint 19.

## Backend Checklist

- [ ] `BE-18.1` Implement myths export path nếu chưa hoàn chỉnh.
- [ ] `BE-18.2` Implement story arc export packs.
- [ ] `BE-18.3` Implement highlight reel manifests hoặc equivalent creator metadata.
- [ ] `BE-18.4` Build unified bundle assembly flow.
- [ ] `BE-18.5` Add provenance/version metadata cho từng artifact.
- [ ] `BE-18.6` Add tests cho bundle integrity và export contracts.

## Frontend Checklist

- [ ] `FE-18.1` Implement creator export entry point rõ ràng.
- [ ] `FE-18.2` Hiển thị bundle contents trước/sau export.
- [ ] `FE-18.3` Implement artifact browsing/download states.
- [ ] `FE-18.4` Cross-link export flows với story arcs, mythology và branches.
- [ ] `FE-18.5` Verify empty/error/partial export states.
- [ ] `FE-18.6` Giữ regular viewer UI không bị overload bởi creator tooling.

## DevOps Checklist

- [ ] `DO-18.1` Chốt retention policy cho artifact bundles.
- [ ] `DO-18.2` Verify local filesystem path và optional remote path đều usable.
- [ ] `DO-18.3` Review storage cost của creator bundles.
- [ ] `DO-18.4` Tạo smoke export suite cho myths/arcs/highlights.
- [ ] `DO-18.5` Chuẩn bị publish/runbook cho artifact recovery.
- [ ] `DO-18.6` Verify artifact metadata đủ cho audit/support.

## Demo & Sign-off

- Demo export một creator bundle đầy đủ từ world hoặc branch.
- Demo myths/arcs/highlights link với nhau trong bundle.
- [ ] Acceptance criteria được review đủ.
- [ ] Gate J có đủ bằng chứng cả runtime flexibility lẫn creator publishing.
- [ ] Carry-over items được ghi sang Sprint 19 hoặc `MASTER-BACKLOG.md`.
- Sign-off owners: Project lead + product lead + backend lead.
