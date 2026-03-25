# Sprint 17 – Per-agent Model Profiles, Local LLM & Multi-provider Settings

## Sprint Metadata

| Field | Value |
| --- | --- |
| Phase | Phase 9 – Runtime Flexibility & Creator Publishing |
| Milestone Gate | Gate J – Creator Runtime Ready |
| Suggested Duration | 2 tuần |
| Primary Validation Signal | Runtime chạy được với nhiều provider/profile paths và user nâng cao chọn được profile theo nhóm agent mà không phá simple path |
| Source Backlog IDs | `ADW-S17-BA-01`, `ADW-S17-BE-01`, `ADW-S17-FE-01`, `ADW-S17-DO-01` |

## Sprint Goal

Hoàn thiện runtime flexibility để world complexity tăng lên mà hệ thống không bị khóa vào một provider/profile duy nhất.

## Business Objective

Cho maintainer và advanced creator chọn provider/model path phù hợp theo mục tiêu chất lượng, cost và latency, đồng thời mở local LLM như một lựa chọn khả dụng.

## Business Value

- Giảm rủi ro vendor lock-in ở tầng runtime.
- Mở đường cho world styles/workloads khác nhau dùng profile khác nhau.
- Tăng khả năng self-host và experimentation qua local LLM path.

## In Scope

- Per-agent model profiles.
- Provider settings cho cloud/local.
- Local LLM path.
- Provider compatibility matrix.
- Runtime profile inspection.

## Out of Scope

- Public model marketplace.
- Full auto-routing phức tạp theo mọi metric.
- Community sharing của provider presets.
- Creator export bundles.

## Primary User Stories

- Với vai trò **maintainer**, tôi muốn cấu hình provider/profile theo nhóm agent.
- Với vai trò **advanced creator**, tôi muốn chạy local LLM nếu không muốn phụ thuộc cloud.
- Với vai trò **operator**, tôi muốn biết profile nào đang active trên world nào.

## Acceptance Criteria

- [ ] App chạy được với ít nhất 2 cloud provider paths và 1 local path.
- [ ] Có thể chọn profile global hoặc theo nhóm agent.
- [ ] Runtime profile inspection hiển thị đúng settings thật.
- [ ] Simple default path vẫn giữ được cho user chỉ cần 1 key + 1 provider.

## Dependencies

- AgentModel abstraction đã ổn từ các sprint trước.
- Settings/config system đủ trưởng thành để hỗ trợ nhiều profile.
- Observability path đo được latency/cost theo provider.

## Sprint Task Board

| Task ID | Stream | Summary | Priority | Estimate |
| --- | --- | --- | --- | --- |
| ADW-S17-BA-01 | BA | Chốt profile matrix và user-facing settings model cho providers | P1 | S |
| ADW-S17-BE-01 | Backend | Implement per-agent profiles, local LLM path và provider routing | P1 | XL |
| ADW-S17-FE-01 | Frontend | Implement provider settings UI và runtime profile inspection | P1 | L |
| ADW-S17-DO-01 | DevOps | Thiết lập provider smoke matrix và local profile ops notes | P2 | M |

## Risks & Control Notes

- Profile matrix quá phức tạp sẽ phá simple path.
- Local LLM contract không rõ sẽ tạo nhiều bug support khó debug.
- Kết quả thế giới có thể drift mạnh giữa profile nếu không có smoke worlds chuẩn.

## BA Checklist

- [ ] `BA-17.1` Chốt global profile vs per-agent-group model.
- [ ] `BA-17.2` Chốt supported provider set của phase này.
- [ ] `BA-17.3` Chốt default-safe path cho user phổ thông.
- [ ] `BA-17.4` Chốt acceptance criteria cho local LLM path.
- [ ] `BA-17.5` Chốt visibility rules cho runtime profile inspection.
- [ ] `BA-17.6` Chuẩn bị handoff requirements cho creator export suite ở Sprint 18.

## Backend Checklist

- [ ] `BE-17.1` Implement settings resolution cho global/per-group profiles.
- [ ] `BE-17.2` Implement provider adapters cần cho phase này.
- [ ] `BE-17.3` Implement local LLM health/check contract.
- [ ] `BE-17.4` Expose runtime profile inspection payloads.
- [ ] `BE-17.5` Add compatibility/smoke tests cho provider matrix.
- [ ] `BE-17.6` Verify fallback path nếu provider/profile fail.

## Frontend Checklist

- [ ] `FE-17.1` Implement provider/profile settings screens hoặc panels.
- [ ] `FE-17.2` Hiển thị active runtime profile theo world hoặc agent group.
- [ ] `FE-17.3` Giữ default flow ngắn gọn cho user chỉ dùng 1 provider.
- [ ] `FE-17.4` Implement validation/error states cho profile config.
- [ ] `FE-17.5` Feature-gate nâng cao để không làm rối main UX.
- [ ] `FE-17.6` Verify settings persistence và refresh behavior.

## DevOps Checklist

- [ ] `DO-17.1` Thiết lập smoke matrix cho cloud/local providers.
- [ ] `DO-17.2` Viết ops notes cho local LLM profile path.
- [ ] `DO-17.3` Theo dõi latency/cost deltas theo provider.
- [ ] `DO-17.4` Verify fallback behavior khi provider chết hoặc timeout.
- [ ] `DO-17.5` Tạo demo matrix world/provider cho review.
- [ ] `DO-17.6` Review secret/config handling cho nhiều providers.

## Demo & Sign-off

- Demo chuyển giữa nhiều provider/profile paths.
- Demo local LLM path và runtime profile inspection.
- [ ] Acceptance criteria được review đủ.
- [ ] Simple path vẫn không bị regression.
- [ ] Carry-over items được ghi sang Sprint 18 hoặc `MASTER-BACKLOG.md`.
- Sign-off owners: Project lead + backend lead + DevOps lead.
