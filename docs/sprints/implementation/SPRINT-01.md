# Sprint 01 – Implementation Companion

## Implementation Intent

Sprint 01 khóa **world model V1** và persistence core. Mục tiêu không phải richness, mà là vocabulary canon và DB path ổn định để Sprint 02–04 build lên.

## Build Slices

- SQLite schema cho 7 core tables.
- Migration/init flow.
- Database-per-world path.
- Repository layer tối thiểu.
- Seed world không dùng LLM.

## Backend Implementation

- Implement tables: `worlds`, `regions`, `locations`, `civilizations`, `settlements`, `events`, `eras`.
- Giữ `affected_entities` JSON cho soft refs ngay từ `events`.
- Tạo repository interfaces đủ cho read/write world summary và events.
- Chọn migration/version strategy đơn giản nhưng explicit.

## Frontend Implementation

- Tạo world summary shell từ `GET /worlds/current`.
- Chưa cần UI richness; chỉ verify world summary data path có thật.

## DevOps / Quality

- Smoke DB init trên first run.
- Verify restart đọc lại world seed.
- Standardize `data/world-{name}.db` path và cleanup policy local.

## Contracts To Freeze

- `GET /worlds/current` summary fields baseline.
- Database naming convention.
- Canon entity glossary V1.

## Verification

- Tạo world seed thành công.
- Restart app vẫn đọc đúng current world.
- Không còn table creep sang `religions/cultures/resources/creatures`.

## Handoff To Sprint 02

- Event pipeline sẽ append vào schema hiện tại, không mở table mới.
- Summary endpoint được xem như source of truth cho overview shell.
- Soft-reference strategy là mặc định cho entity chưa có table.
