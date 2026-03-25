# Sprint 08 – Implementation Companion

## Implementation Intent

Sprint 08 thêm **macro causality**. Mục tiêu là tăng variety mà không làm coherence collapse. Đây là sprint cần tuning nhiều nhất, không nên chase feature count.

## Build Slices

- Ecology Agent.
- Economy Agent.
- Chaos Agent.
- Propagation rules cho scarcity/conflict/collapse.
- Balance/tuning loop.

## Backend Implementation

- Implement propagation-aware event generation.
- Expand Guardian rules cho macro chains.
- Add scoring/tuning hooks để reject rate và chaos rate quan sát được.

## Frontend Implementation

- Extend feed/timeline labels cho event types mới.
- Add minimal filters/impact badges cho macro events.

## DevOps / Quality

- Long-run simulation tests.
- Cost and instability monitoring.
- Compare runs trước/sau tuning.

## Contracts To Freeze

- Macro event categories.
- Propagation rule semantics.
- Coherence metrics thresholds cho expanded simulation.

## Verification

- Event variety tăng nhưng invalid spike vẫn trong ngưỡng.
- Trade/ecology/scarcity tạo hậu quả liên hoàn có thể giải thích được.
- World vẫn readable trên observer surfaces.

## Handoff To Sprint 09

- Visualization layer sẽ cần map/civ projections từ macro state, không từ ad hoc heuristics.
