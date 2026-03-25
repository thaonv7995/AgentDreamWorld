# Sprint 12 – Implementation Companion

## Implementation Intent

Sprint 12 creates **multi-world foundation**, not full multi-world product. The implementation must isolate world lifecycle assumptions in data/runtime layers before UX expands in Sprint 13–14.

## Build Slices

- Multi-world metadata model.
- Current-world abstraction.
- Snapshot/fork hooks.
- Ops runbook baseline.

## Backend Implementation

- Add world registry/current world indirection.
- Store world metadata separately from world state where appropriate.
- Prepare fork/snapshot hooks without committing to final UX semantics yet.

## Frontend Implementation

- Minimal selector/list shell only.
- Do not over-design multi-world manager yet.

## DevOps / Quality

- Backup/restore flows for multiple worlds.
- World growth monitoring labels and cleanup thinking.
- Recovery drills for snapshot metadata path.

## Contracts To Freeze

- World metadata schema.
- Current-world selection semantics.
- Snapshot/fork provenance fields baseline.

## Verification

- Current-world UX still works unchanged.
- Multi-world metadata survives restart/reload.
- No hard-coded “single world forever” assumptions remain in core flows.

## Handoff To Sprint 13

- Sprint 13 can productize world manager on top of this foundation without reworking storage model.
