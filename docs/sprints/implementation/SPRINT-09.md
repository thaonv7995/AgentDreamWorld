# Sprint 09 – Implementation Companion

## Implementation Intent

Sprint 09 chuyển từ text-first sang **geography-first exploration**. Map và Civilization Viewer phải dùng data thật, không fake layout hoặc sample civ detail.

## Build Slices

- Region/world map beta.
- Territory ownership projection.
- Civilization detail projection.
- Settlement distribution surfaces.

## Backend Implementation

- Build map projection from world model and region/location data.
- Add civ detail read model with history/ownership/settlements summary.
- Keep map abstraction simple; stylized is acceptable, hard-coded is not.

## Frontend Implementation

- Render map beta and civ viewer from projections.
- Add navigation from feed/timeline to civ/geography detail.
- Handle sparse worlds gracefully.

## DevOps / Quality

- Perf budget cho map rendering.
- Preview snapshots for visual QA.
- Dataset seeds with enough spatial diversity.

## Contracts To Freeze

- Map projection shape.
- Civilization viewer payload.
- Ownership/territory semantics.

## Verification

- Map renders multiple worlds without manual tweaking.
- Civilization viewer matches backend state.
- Navigation across feed -> civ -> map works.

## Handoff To Sprint 10

- Mythology Browser and graph will build on entity linking started here.
- Map/civ viewer become anchor surfaces for later shared/community UX.
