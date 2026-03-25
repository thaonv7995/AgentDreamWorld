# Sprint 13 – Implementation Companion

## Implementation Intent

Sprint 13 turns multi-world foundation into **usable product UX**. The key is state isolation and a short happy path for world creation/selection.

## Build Slices

- World manager UI/API.
- Create/select/archive flows.
- Preset metadata and lifecycle states.
- Current world switching.

## Backend Implementation

- Build world lifecycle APIs with clear state transitions.
- Persist presets as data, not implicit names in UI.
- Protect active runtime jobs during world switching.

## Frontend Implementation

- World manager shell and create flow.
- Selection/switching UX.
- Archive state presentation and empty/single/multi-world cases.

## DevOps / Quality

- Smoke create/select/archive flows.
- Storage growth review across multiple worlds.
- Backup naming aligned to `world_id`.

## Contracts To Freeze

- World lifecycle API.
- Preset metadata schema.
- Current-world switch semantics.

## Verification

- 2–3 worlds can coexist and switch cleanly.
- Switching does not leak feed/config/state.
- Single-world path remains simple.

## Handoff To Sprint 14

- Pace controls and inspectors will bind to the world manager and current-world selection surfaces from this sprint.
