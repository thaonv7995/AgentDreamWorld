# Sprint 11 – Implementation Companion

## Implementation Intent

Sprint 11 only adds **advanced profile and advanced observability**. It must not backfill baseline telemetry that should already exist, and it must not make SQLite path second-class.

## Build Slices

- Optional Postgres profile.
- Optional Redis hooks.
- Advanced metrics/trace/dashboard layer.
- Perf/load baseline.

## Backend Implementation

- Separate config/profile resolution cleanly.
- Reuse `tick_log`/`llm_call_log` instead of building parallel telemetry truths.
- Add instrumentation/export surfaces for advanced ops.

## Frontend Implementation

- Minimal debug/admin health summary only.
- Keep advanced/admin views feature-gated.

## DevOps / Quality

- Compose stack for advanced profile.
- Baseline load tests.
- Backup/restore baseline for advanced data paths.

## Contracts To Freeze

- Profile selection semantics.
- Advanced metrics names/meaning.
- SQLite-first default guarantee.

## Verification

- Default path still works without advanced stack.
- Advanced profile reads same truths as baseline logs/reports.
- Perf/load notes documented for future scale decisions.

## Handoff To Sprint 12

- Multi-world foundation must work on default path first, then optionally on advanced profile.
