# Sprint 17 – Implementation Companion

## Implementation Intent

Sprint 17 completes **runtime flexibility**. Provider/profile choices must be explicit, inspectable, and safe; local LLM must be treated as a supported path, not a side experiment.

## Build Slices

- Per-agent model profiles.
- Multi-provider settings.
- Local LLM path.
- Runtime profile inspection.

## Backend Implementation

- Resolve config at global and agent-group levels.
- Keep provider adapters behind the same `AgentModel` contract.
- Add local provider health and fallback semantics.

## Frontend Implementation

- Settings UI for provider/profile selection.
- Profile inspection for active world/runtime.
- Preserve simple default config flow for non-advanced users.

## DevOps / Quality

- Provider smoke matrix.
- Secrets/config review for multiple providers.
- Local provider setup and support notes.

## Contracts To Freeze

- Provider/profile config schema.
- Runtime profile inspection payload.
- Local LLM health contract.

## Verification

- At least 2 cloud and 1 local path are runnable.
- Provider fallback behavior is visible and understandable.
- Default path still works with minimal config.

## Handoff To Sprint 18

- Creator publishing bundles can now annotate which runtime/profile generated the artifacts.
