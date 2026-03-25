# Sprint 05 – Implementation Companion

## Implementation Intent

Sprint 05 hoàn thiện **history navigation** và **minimum intervention**. Timeline là trọng tâm; God Mode lite chỉ được làm ở mức preset, không mở custom control sâu.

## Build Slices

- Timeline projection + UI.
- Pause/resume/manual tick controls.
- God Mode lite presets.
- Better summaries cho world/era/civ.

## Backend Implementation

- Build timeline grouping/zoom-ready projections.
- Add simulation control endpoints/state machine.
- Implement preset intervention path qua cùng Guardian/Historian pipeline.

## Frontend Implementation

- Timeline screen với range/marker interactions.
- Control bar cho pause/resume/manual tick.
- God Mode lite panel với preset actions.

## DevOps / Quality

- Demo profile cho history navigation.
- Verify simulation controls không race với active ticks.
- Intervention smoke tests.

## Contracts To Freeze

- Timeline projection shape.
- Simulation control semantics.
- God Mode lite preset request/response contracts.

## Verification

- Tua lại history usable.
- Pause/resume không corrupt state.
- Preset intervention tạo event hợp lệ và visible trên timeline/feed.

## Handoff To Sprint 06

- Exports phải reuse timeline/history data đã readable ở sprint này.
- Control state machine trở thành baseline cho later pace controls.
