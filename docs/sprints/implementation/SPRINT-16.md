# Sprint 16 – Implementation Companion

## Implementation Intent

Sprint 16 makes **alternate timelines real**. Branches must behave like first-class worlds with provenance, not like ad hoc copies.

## Build Slices

- World forking.
- Branch/mainline compare.
- Snapshot sharing.
- Provenance and audit metadata.

## Backend Implementation

- Fork at year/era/event checkpoints with explicit provenance.
- Keep mainline and branch isolation in runtime scheduling and state storage.
- Build compare projections that summarize divergence, not raw diffs only.

## Frontend Implementation

- Fork flow from timeline/checkpoint surfaces.
- Branch navigation and compare views.
- Snapshot share/export states.

## DevOps / Quality

- Retention and cleanup policy for branches/snapshots.
- Restore drills for branch/snapshot recovery.
- Storage growth monitoring.

## Contracts To Freeze

- Branch provenance schema.
- Compare projection shape.
- Snapshot artifact metadata.

## Verification

- A branch can diverge and continue independently.
- Compare view explains changed civilizations/regions/events.
- Snapshot sharing is portable and auditable.

## Handoff To Sprint 17

- Runtime flexibility and creator export pipeline will consume world/branch artifacts created here.
