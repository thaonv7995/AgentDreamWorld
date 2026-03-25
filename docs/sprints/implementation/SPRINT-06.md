# Sprint 06 – Implementation Companion

## Implementation Intent

Sprint 06 chốt **MVP release candidate**. Mọi việc trong sprint này phải trả lời câu hỏi: user có thể cài, chạy, xem world và export content usable chưa.

## Build Slices

- Wiki export.
- Annals export.
- Single-binary mode.
- Config/error hardening.
- MVP packaging/release notes.

## Backend Implementation

- Implement export assembly từ canonical data và summaries.
- Serve static frontend từ backend trong single-binary mode.
- Normalize config/error paths cho release use.

## Frontend Implementation

- Export entry points và status states.
- Polish observer/history path để bỏ mock-only assumptions cuối cùng.
- Verify single-binary mode assets/load path.

## DevOps / Quality

- Build release artifact.
- Smoke export flow trên release build.
- QA checklist theo `MVP-SPEC` DoD.

## Contracts To Freeze

- Export output structure cho wiki/annals.
- Single-binary run contract.
- MVP install/run instructions.

## Verification

- Sau 5–10 phút, app có history readable.
- Export tạo file usable.
- Single-binary mode chạy được trên local target path.

## Handoff To Sprint 07

- Từ đây trở đi là V2+/post-MVP richness; không được quay lại phá V1 release path.
- Export structure ở sprint này là nền của later myth/highlight bundles.
