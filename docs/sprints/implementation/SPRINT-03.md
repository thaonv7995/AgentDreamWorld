# Sprint 03 – Implementation Companion

## Implementation Intent

Sprint 03 phải tạo được **first real world**, nhưng vẫn trong boundaries V1. Chìa khóa là reuse tick pipeline đã khóa ở Sprint 02 và thêm genesis orchestration, không tạo “special path” tách biệt.

## Build Slices

- Creator/Civilization/Storyteller V1.
- Genesis runner 50–200 ticks.
- Event list/filter API.
- API contract types và contract tests.
- Snapshot/replay cho genesis path.

## Backend Implementation

- Build prompt/context per agent từ same runtime abstractions.
- Genesis runner dùng world boundaries config và active-agent selection rules.
- Persist world summaries đủ để frontend Sprint 04 consume ngay.
- Expose filterable events API với paging/meta ổn định.

## Frontend Implementation

- Genesis progress/loading path.
- Feed/overview shell consume API thật.
- Filter skeleton theo contract đã khóa.

## DevOps / Quality

- Mock genesis smoke path phải deterministic.
- Live genesis path có timeout/retry/cost tracking.
- Snapshot golden outputs cho mock genesis.

## Contracts To Freeze

- `WorldSummary`, `WorldEvent`, `EventsResponse`, `TimelineEra`.
- Feed/timeline projection fields.
- Genesis boundaries và hard limits.

## Verification

- Cùng fixture genesis -> cùng snapshot.
- World sau genesis không rỗng và nằm trong scope V1.
- Feed API usable cho frontend mà không cần mock adapters.

## Handoff To Sprint 04

- Frontend Sprint 04 chỉ consume projections đã khóa, không tự suy field.
- Genesis world sample trở thành demo dataset mặc định cho observer UI.
