# Sprint 15 – Advanced God Mode & Story Arc Highlighter

## Sprint Metadata

| Field | Value |
| --- | --- |
| Phase | Phase 8 – Alternate Timelines & Creator Control |
| Milestone Gate | Gate I – Alternate Timeline Ready |
| Suggested Duration | 2 tuần |
| Primary Validation Signal | Creator can thiệp vào world có kiểm soát và hệ thống tự highlight được story arcs đáng khai thác |
| Source Backlog IDs | `ADW-S15-BA-01`, `ADW-S15-BE-01`, `ADW-S15-FE-01`, `ADW-S15-DO-01` |

## Sprint Goal

Nâng God Mode từ preset tối thiểu lên creator control có guardrails, đồng thời tạo story curation layer.

## Business Objective

Cho creator can thiệp sâu hơn vào world mà không làm simulation thành hỗn loạn ngẫu nhiên, và giúp họ tìm ra các arc mạnh nhất để làm content.

## Business Value

- Tăng khả năng tạo “what-if” đáng xem trước cả khi mở full forking.
- Biến world history thành material có thể curate, không chỉ đọc thủ công.
- Mở đường cho alternate timeline và creator publishing pipeline.

## In Scope

- Advanced God Mode.
- Guardrails cho interventions.
- Story Arc Highlighter.
- Arc summary cards và cross-links.

## Out of Scope

- World forking.
- Snapshot sharing.
- Public gallery/community.
- Full provider profile routing.

## Primary User Stories

- Với vai trò **creator**, tôi muốn trigger intervention sâu hơn preset V1.
- Với vai trò **writer/content creator**, tôi muốn hệ thống chỉ ra các story arcs mạnh nhất.
- Với vai trò **maintainer**, tôi muốn interventions vẫn bị guardrail để coherence không vỡ.

## Acceptance Criteria

- [ ] Advanced God Mode có intensity/scope/target semantics rõ.
- [ ] Interventions để lại hậu quả truy vết được trong timeline/log.
- [ ] Story Arc Highlighter tạo ra arc cards readable.
- [ ] Guardrails chặn các intervention phá world state ngoài boundary đã chốt.

## Dependencies

- Sprint 14 đã có pace/log/config tooling để inspect hậu quả.
- Guardian/Historian rules đủ trưởng thành để absorb intervention phức tạp hơn.
- Taxonomy entities/events ổn định cho arc extraction.

## Sprint Task Board

| Task ID | Stream | Summary | Priority | Estimate |
| --- | --- | --- | --- | --- |
| ADW-S15-BA-01 | BA | Chốt guardrails cho Advanced God Mode và taxonomy story arcs | P1 | S |
| ADW-S15-BE-01 | Backend | Implement advanced interventions và story arc extraction | P1 | XL |
| ADW-S15-FE-01 | Frontend | Implement Advanced God Mode UI và story arc surfaces | P1 | L |
| ADW-S15-DO-01 | DevOps | Chạy coherence/cost review cho advanced intervention paths | P2 | M |

## Risks & Control Notes

- Intervention quá mạnh sẽ làm world mất readability nếu guardrails yếu.
- Arc extraction dễ trở thành heuristic mơ hồ; phải giữ contract rõ và explainable.
- UI phải tách rõ “viewer mode” với “creator control mode”.

## BA Checklist

- [ ] `BA-15.1` Chốt intervention taxonomy và semantics cho scope/intensity.
- [ ] `BA-15.2` Chốt target selection rules theo world/region/civilization.
- [ ] `BA-15.3` Chốt story arc categories và scoring inputs.
- [ ] `BA-15.4` Chốt acceptance criteria cho creator control path.
- [ ] `BA-15.5` Review explainability requirements cho arc cards.
- [ ] `BA-15.6` Chuẩn bị handoff cho alternate timeline compare ở Sprint 16.

## Backend Checklist

- [ ] `BE-15.1` Implement Advanced God Mode request model và validation.
- [ ] `BE-15.2` Reuse Guardian/Historian path để interventions không bypass rules.
- [ ] `BE-15.3` Implement story arc extraction/scoring pipeline.
- [ ] `BE-15.4` Link arcs với timeline, mythology và canonical events.
- [ ] `BE-15.5` Add tests cho intervention guardrails và arc quality baselines.
- [ ] `BE-15.6` Expose explainable fields cho arc summary cards.

## Frontend Checklist

- [ ] `FE-15.1` Implement Advanced God Mode form/controls với safe defaults.
- [ ] `FE-15.2` Hiển thị intervention preview hoặc consequence hints nếu có.
- [ ] `FE-15.3` Implement Story Arc Highlighter panels/cards.
- [ ] `FE-15.4` Cross-link arcs sang feed, timeline và mythology surfaces.
- [ ] `FE-15.5` Feature-gate creator controls khỏi regular viewer path.
- [ ] `FE-15.6` Verify loading/error states cho interventions và arc generation.

## DevOps Checklist

- [ ] `DO-15.1` Chạy intervention regression set cho coherence.
- [ ] `DO-15.2` Theo dõi cost/time của advanced intervention runs.
- [ ] `DO-15.3` Review reject reasons mới do guardrails sinh ra.
- [ ] `DO-15.4` Tạo demo seeds/worlds phù hợp cho arc extraction showcase.
- [ ] `DO-15.5` Chuẩn bị rollback notes nếu intervention gây instability.
- [ ] `DO-15.6` Verify arc pipeline không làm log/metrics mù đi nguồn gốc event.

## Demo & Sign-off

- Demo Advanced God Mode với ít nhất 2 intervention types.
- Demo Story Arc Highlighter tạo arc cards usable.
- [ ] Acceptance criteria được review đủ.
- [ ] Creator control path giữ coherence trong ngưỡng team chấp nhận.
- [ ] Carry-over items được ghi sang Sprint 16 hoặc `MASTER-BACKLOG.md`.
- Sign-off owners: Project lead + backend lead + product lead.
