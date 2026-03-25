# Sprint 18 – Implementation Companion

## Implementation Intent

Sprint 18 turns exports into a **creator publishing pipeline**. Artifacts must be bundled, named, versioned, and provenance-aware.

## Build Slices

- Myths export.
- Arc export packs.
- Highlight manifests.
- Unified creator bundle.
- Optional remote artifact path.

## Backend Implementation

- Assemble unified bundles from canonical world data, branch metadata, myths, arcs, and highlight manifests.
- Add provenance/version metadata to each artifact.
- Keep remote artifact storage optional behind the same bundle contract.

## Frontend Implementation

- Creator bundle export entry point.
- Bundle contents preview and download states.
- Cross-links from myths/arcs/highlights to export flow.

## DevOps / Quality

- Artifact retention and storage policy.
- Smoke suite for bundle generation.
- Support docs for artifact recovery/re-download.

## Contracts To Freeze

- Creator bundle structure.
- Highlight manifest schema.
- Artifact provenance/version fields.

## Verification

- A creator bundle is usable without manual stitching.
- Myths/arcs/highlights all link back to source world/branch.
- Optional remote path does not change bundle semantics.

## Handoff To Sprint 19

- World packages and community gallery will build on creator bundle/provenance conventions from this sprint.
