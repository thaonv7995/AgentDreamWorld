# Sprint 00 – Implementation Companion

## Implementation Intent

Sprint 00 chỉ được phép tạo **walking skeleton**, không xây logic simulation thật. Mọi quyết định kỹ thuật ở sprint này phải tối ưu cho việc mở rộng ở Sprint 01–02, không tối ưu sớm.

## Build Slices

- Rust workspace + `ai-dreams-server` binary.
- React/Vite frontend shell.
- Shared dev script và `.env.example`.
- Process modes: `full`, `api-only`, `sim-only`, `single-tick`.
- Walking skeleton: `POST /tick` stub -> persist stub event -> `GET /events` -> UI render.

## Backend Implementation

- Tạo crate boundaries tối thiểu: `app`, `http`, `runtime`, `infra`.
- Expose health endpoint và stub tick/event endpoints.
- Chọn config loading ngay từ đầu theo env + fallback local defaults.
- Dùng channel hoặc interface stub cho simulation control để không gắn HTTP vào engine trực tiếp.

## Frontend Implementation

- Tạo app shell với layout đủ cho feed/status area.
- Gọi stub API thật, không hard-code JSON trong component.
- Có loading/error/empty states ngay từ skeleton.

## DevOps / Quality

- Chốt local commands: build, dev, smoke.
- CI tối thiểu: install, type/lint/build, backend test shell.
- README và DEV-SETUP phải phản ánh runnable scaffold thật.

## Contracts To Freeze

- Port/backend URL local.
- Process mode CLI contract.
- Stub event shape tối thiểu cho walking skeleton.

## Verification

- `ai-dreams-server` chạy ở `api-only`.
- Frontend render được event từ API thật.
- Single command local dev path hoạt động trên máy mới.

## Handoff To Sprint 01

- Repo structure không đổi lớn nữa.
- Config path và mode names được xem như stable baseline.
- Stub event/world flow đủ chỗ để thay bằng schema thật.
