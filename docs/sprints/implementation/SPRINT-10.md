# Sprint 10 – Implementation Companion

## Implementation Intent

Sprint 10 biến world thành **linked lore system**. Browser và graph phải mang giá trị khám phá, không chỉ là index của entity names.

## Build Slices

- Mythology Browser.
- Knowledge Graph beta.
- Entity linking between civ/myth/religion/event/region/settlement.
- Richer export artifacts from linked data.

## Backend Implementation

- Build graph-friendly projections and node/edge taxonomy.
- Maintain explainable links from source events and summaries.
- Keep graph bounded for V2 world sizes.

## Frontend Implementation

- Browser views for myths/cults/prophecies.
- Graph exploration with safe defaults and filters.
- Cross-navigation among graph, timeline, map, and civ detail.

## DevOps / Quality

- Measure graph query latency and render perf.
- Visual regression snapshots for graph/browser.
- Sample worlds with dense mythic links.

## Contracts To Freeze

- Graph node/edge schema.
- Mythology browser taxonomy.
- Linked-export semantics.

## Verification

- Graph usable on at least target V2 world size.
- Myth browser navigates to real events/entities.
- Linked exports preserve core relationships.

## Handoff To Sprint 11

- Advanced profile must observe graph/query costs but not force infra migration.
