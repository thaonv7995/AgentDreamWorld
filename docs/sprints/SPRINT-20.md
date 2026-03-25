# Sprint 20 – Collaborative Viewing, Shared Sessions & Social Safety Rails

## Sprint Metadata

| Field | Value |
| --- | --- |
| Phase | Phase 10 – Community & Collaboration |
| Milestone Gate | Gate K – Community Vision Ready |
| Suggested Duration | 2 tuần |
| Primary Validation Signal | 2+ user có thể cùng xem một world/session với feed/timeline nhất quán và intervention permissions rõ ràng |
| Source Backlog IDs | `ADW-S20-BA-01`, `ADW-S20-BE-01`, `ADW-S20-FE-01`, `ADW-S20-DO-01` |

## Sprint Goal

Đóng vòng documented vision bằng collaborative viewing có guardrails và audit trail rõ ràng.

## Business Objective

Cho nhiều người cùng quan sát một world, cùng thấy evolution/history giống nhau, và chỉ những ai có quyền mới được trigger interventions trong shared session.

## Business Value

- Chạm trực tiếp phần Collaborative Viewing trong vision docs.
- Biến community layer từ gallery thụ động thành trải nghiệm sống.
- Đưa project tới “full vision baseline” thay vì chỉ là creator workstation cá nhân.

## In Scope

- Collaborative viewing sessions.
- Shared Dream Feed / Timeline state.
- Session roles và permissions.
- Audit trail cho interventions.
- Conflict handling cho concurrent actions.

## Out of Scope

- MMO-scale multiplayer backend.
- Chat/social network đầy đủ.
- Marketplace hoặc economy community.
- Open-ended collaborative authoring ngoài scope session rules.

## Primary User Stories

- Với vai trò **viewer**, tôi muốn cùng bạn bè xem một world đang chạy.
- Với vai trò **operator**, tôi muốn trigger event trong shared session theo quyền được cấp.
- Với vai trò **moderator/maintainer**, tôi muốn audit được ai đã làm gì trong session.

## Acceptance Criteria

- [ ] 2+ user thấy cùng một shared feed/timeline.
- [ ] Permission model cho viewer/operator/moderator hoạt động đúng.
- [ ] Shared interventions có audit trail rõ.
- [ ] Concurrent actions không làm world/session rơi vào state mơ hồ.

## Dependencies

- Sprint 19 đã có shared packages/gallery/provenance.
- Multi-world runtime và current-world isolation đã vững từ Sprint 13–16.
- Observability/audit infrastructure đủ tốt để support session trail.

## Sprint Task Board

| Task ID | Stream | Summary | Priority | Estimate |
| --- | --- | --- | --- | --- |
| ADW-S20-BA-01 | BA | Chốt session roles, permissions và safety rails cho collab mode | P1 | S |
| ADW-S20-BE-01 | Backend | Implement shared session runtime, audit trail và intervention conflict handling | P1 | XL |
| ADW-S20-FE-01 | Frontend | Implement collaborative viewing UI, presence và shared control states | P1 | XL |
| ADW-S20-DO-01 | DevOps | Thiết lập ops, rate-limit và abuse/runbook cho collaborative sessions | P2 | M |

## Risks & Control Notes

- Collaborative mode rất dễ trượt thành real-time game backend nếu boundary không giữ chặt.
- Permission model phải đơn giản nhưng đủ an toàn.
- Audit trail là bắt buộc, không phải nice-to-have.

## BA Checklist

- [ ] `BA-20.1` Chốt session role model: viewer / operator / moderator.
- [ ] `BA-20.2` Chốt permission matrix cho shared interventions.
- [ ] `BA-20.3` Chốt session UX boundary để không biến app thành social app full-stack.
- [ ] `BA-20.4` Chốt acceptance criteria cho Gate K.
- [ ] `BA-20.5` Review abuse scenarios và safety rails.
- [ ] `BA-20.6` Chuẩn bị full-vision sign-off checklist sau Sprint 20.

## Backend Checklist

- [ ] `BE-20.1` Implement shared session model/runtime abstraction.
- [ ] `BE-20.2` Sync shared feed/timeline state cho nhiều viewers.
- [ ] `BE-20.3` Implement role/permission enforcement cho interventions.
- [ ] `BE-20.4` Implement audit trail và session event logs.
- [ ] `BE-20.5` Implement conflict handling cho concurrent actions.
- [ ] `BE-20.6` Add tests cho session consistency và permission paths.

## Frontend Checklist

- [ ] `FE-20.1` Implement session join/view flow.
- [ ] `FE-20.2` Hiển thị shared session state và presence tối thiểu.
- [ ] `FE-20.3` Implement permission-aware controls cho interventions.
- [ ] `FE-20.4` Hiển thị audit/history state trong session nếu cần.
- [ ] `FE-20.5` Verify viewer path không thấy controls không có quyền.
- [ ] `FE-20.6` Verify error/reconnect/conflict states cho collaborative viewing.

## DevOps Checklist

- [ ] `DO-20.1` Chốt rate limits và abuse mitigations cho sessions.
- [ ] `DO-20.2` Review observability và audit requirements cho shared mode.
- [ ] `DO-20.3` Tạo runbook cho moderation/escalation path.
- [ ] `DO-20.4` Chạy load test tối thiểu cho nhiều viewers trong một session.
- [ ] `DO-20.5` Chuẩn bị rollback/kill-switch cho collab mode.
- [ ] `DO-20.6` Verify session safety rails không phá default solo path.

## Demo & Sign-off

- Demo 2+ user cùng xem một world/session.
- Demo permission model và audit trail cho shared intervention.
- [ ] Acceptance criteria được review đủ.
- [ ] Gate K chạm được baseline full vision đã mô tả trong `ai-dreams-vision.md`.
- [ ] Carry-over items sau Sprint 20 được ghi như post-vision backlog riêng.
- Sign-off owners: Project lead + backend lead + DevOps lead + product lead.
