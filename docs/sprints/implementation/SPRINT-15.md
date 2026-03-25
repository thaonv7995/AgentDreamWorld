# Sprint 15 – Implementation Companion

## Implementation Intent

Sprint 15 introduces **creator-grade intervention** and **story curation**. The implementation must keep interventions on the same governed simulation path, never as admin bypasses.

## Build Slices

- Advanced God Mode.
- Intervention guardrails.
- Story Arc Highlighter.
- Arc cards and links.

## Backend Implementation

- Model interventions as proposals or controlled commands that still hit validation/canonicalization.
- Build arc extraction from canonical events, summaries, and myth layers.
- Keep arc scoring explainable and traceable.

## Frontend Implementation

- Advanced God Mode forms with safe defaults.
- Arc cards/panels linked into timeline/browser surfaces.
- Clear separation between viewer and creator tooling.

## DevOps / Quality

- Coherence regression set for interventions.
- Cost/latency review for intervention-heavy runs.
- Demo worlds chosen for strong arc emergence.

## Contracts To Freeze

- Advanced intervention request schema.
- Arc card/output schema.
- Explainability fields for arcs.

## Verification

- Interventions leave visible, traceable consequences.
- Guardrails block destructive/invalid changes.
- Arc highlighter produces usable story slices.

## Handoff To Sprint 16

- Forking and compare UX will use interventions/arcs as key checkpoints and narrative anchors.
