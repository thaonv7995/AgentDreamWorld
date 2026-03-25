# Sprint 07 – Implementation Companion

## Implementation Intent

Sprint 07 thêm **cultural/mythic depth** nhưng không được làm context nổ tung. Era summaries là phần bắt buộc vì không có chúng thì V2 agents sẽ làm prompt size mất kiểm soát.

## Build Slices

- Culture Agent.
- Myth Agent.
- Era summaries.
- Myth/culture projections baseline.

## Backend Implementation

- Implement Culture/Myth agents qua runtime abstractions hiện có.
- Persist era summaries như compressed context artifacts.
- Dùng soft refs hoặc minimal projections trước khi đòi table explosion.

## Frontend Implementation

- Show culture/myth tags và era summary panel.
- Không làm full Mythology Browser ở sprint này.

## DevOps / Quality

- Version prompt/rule sets.
- Soak era transition path.
- Track token/context savings nhờ summaries.

## Contracts To Freeze

- Era summary schema.
- Myth/culture tag projection fields.
- Context selection rules dùng summaries.

## Verification

- Agent context không cần đọc full event log.
- World history bắt đầu có customs/myths readable.
- Era transition không làm context regress mạnh.

## Handoff To Sprint 08

- Ecology/Economy/Chaos phải consume era summaries thay vì bơm raw history vô hạn.
- Myth/culture outputs là inputs cho later browser/export paths.
