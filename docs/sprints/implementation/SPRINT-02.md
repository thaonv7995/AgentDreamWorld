# Sprint 02 – Implementation Companion

## Implementation Intent

Sprint 02 phải tạo được **tick pipeline deterministic enough to debug**. Đây là sprint khóa observability baseline, rule engine baseline và mock provider baseline.

## Build Slices

- `EventProposal` pipeline.
- Manual tick orchestration.
- Declarative Guardian.
- Scoring Historian.
- `llm_call_log`, `tick_log`, CLI report.
- Mock provider + replay-ready path.

## Backend Implementation

- Tách `proposal -> validate -> canonize -> commit` thành pipeline rõ stage.
- Log mọi stage vào metrics/log tables với `PipelineStage`.
- Rule engine đọc files, không hard-code event validation trong code path.
- Historian chỉ score/select/normalize, không invent facts.

## Frontend Implementation

- Debug tick trigger tối thiểu.
- Event list shell đọc event thật sau manual tick.
- Không build polished UI; chỉ phục vụ debug và demo.

## DevOps / Quality

- Mock/live profiles rõ bằng config.
- Timeout + retry + circuit-breaker baseline.
- `report --last N` tổng hợp success/reject/cost/latency.

## Contracts To Freeze

- Tick endpoint contract.
- Raw event vs canonical event semantics.
- `tick_log` / `llm_call_log` column semantics.

## Verification

- Một tick đi hết pipeline bằng mock provider.
- Guardian reject reason đọc được, explainable.
- Historian canonicalization ổn định với fixture lặp lại.

## Handoff To Sprint 03

- Genesis runner phải reuse pipeline này, không tạo loop riêng.
- Replay/snapshot path từ sprint này sẽ là nền của genesis deterministic tests.
- Observability baseline không được defer sang sprint sau.
