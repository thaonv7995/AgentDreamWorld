# Sprint 00 – Repo Scaffold & Delivery Rails

## Sprint Metadata

| Field | Value |
| --- | --- |
| Phase | Phase 0 – Foundation |
| Milestone Gate | Gate A – Scaffold Ready |
| Suggested Duration | 2 tuần |
| Primary Validation Signal | Contributor mới đi từ clone tới first run trong < 30 phút |
| Source Backlog IDs | `ADW-S00-BA-01`, `ADW-S00-BE-01`, `ADW-S00-FE-01`, `ADW-S00-DO-01` |

## Sprint Goal

Biến repo từ trạng thái `docs-only` thành codebase skeleton có thể chạy được ở mức cơ bản.

## Business Objective

Thiết lập nền thực thi để team có thể bắt đầu phát triển thật thay vì chỉ làm việc trên spec. Sprint này phải loại bỏ rủi ro onboarding và tạo ra đường chạy đầu tiên cho backend/frontend.

## Business Value

- Giảm khoảng cách giữa docs và implementation.
- Tạo baseline rõ cho contributor mới.
- Mở khóa toàn bộ các sprint tiếp theo.
- Cho phép planning từ “ý tưởng” sang “delivery”.

## In Scope

- Rust workspace và `crates/server`.
- React + Vite frontend shell.
- `.env.example`.
- `scripts/dev.sh`.
- README/DEV-SETUP cập nhật theo trạng thái runnable thật.
- Build/lint scripts tối thiểu.

## Out of Scope

- World model thật.
- SQLite schema thật.
- Simulation loop thật.
- UI feature thật ngoài app shell.

## Primary User Stories

- Với vai trò **contributor mới**, tôi muốn clone repo và chạy được skeleton để biết môi trường đã sẵn sàng.
- Với vai trò **tech lead**, tôi muốn có cấu trúc repo chuẩn để bắt đầu chia việc cho backend/frontend/devops.
- Với vai trò **developer**, tôi muốn có một flow dev tối thiểu để bắt đầu code mà không phải đoán cấu trúc dự án.

## Acceptance Criteria

- [ ] Repo có Rust workspace và frontend app shell rõ ràng.
- [ ] `cargo run --bin ai-dreams-server` chạy được stub server.
- [ ] `npm run dev` mở được app shell.
- [ ] `.env.example` tồn tại và mô tả đúng biến môi trường tối thiểu.
- [ ] README và DEV-SETUP không còn mô tả sai trạng thái runnable của repo.
- [ ] Contributor mới có thể first-run trong < 30 phút.

## Dependencies

- Bộ docs sản phẩm/kỹ thuật hiện tại đã chốt baseline.
- Team thống nhất cấu trúc repo theo `ai-dreams-technical.md`.
- Có sẵn toolchain Rust và Node trên máy dev.

## Sprint Task Board

| Task ID | Stream | Summary | Priority | Estimate |
| --- | --- | --- | --- | --- |
| ADW-S00-BA-01 | BA | Chốt acceptance criteria scaffold, onboarding path và DoR cho Sprint 01 | P1 | S |
| ADW-S00-BE-01 | Backend | Tạo Rust workspace, binary `ai-dreams-server` và stub endpoint | P1 | M |
| ADW-S00-FE-01 | Frontend | Tạo React + Vite app shell, layout rỗng và API stub | P1 | M |
| ADW-S00-DO-01 | DevOps | Thiết lập `dev.sh`, `.env.example` và CI tối thiểu | P1 | M |

## Risks & Control Notes

- Không để Sprint 00 trôi sang implement domain logic; sprint này chỉ mở đường chạy.
- Nếu scaffold xong nhưng README và DEV-SETUP chưa phản ánh đúng, onboarding vẫn xem như fail.
- CI và local commands phải đơn giản hơn hoàn chỉnh; ưu tiên runnable trước, tối ưu sau.

## BA Checklist

- [ ] `BA-00.1` Đối chiếu `README`, `DEV-SETUP`, `ai-dreams-technical.md` để chốt repo structure mục tiêu của Sprint 00.
- [ ] `BA-00.2` Viết rõ first-run path: clone -> env -> backend run -> frontend run -> verify shell.
- [ ] `BA-00.3` Chốt acceptance criteria chi tiết cho backend shell, frontend shell và local dev flow.
- [ ] `BA-00.4` Chốt definition of ready cho Sprint 01, đặc biệt là các input cần có từ scaffold.
- [ ] `BA-00.5` Review lại toàn bộ docs onboarding để loại bỏ mọi claim “repo đã runnable” nếu chưa được scaffold support.
- [ ] `BA-00.6` Chuẩn bị demo script và sign-off checklist cho Gate A.

## Backend Checklist

- [ ] `BE-00.1` Tạo Rust workspace root và cấu trúc thư mục backend đúng naming convention của dự án.
- [ ] `BE-00.2` Tạo crate/binary `ai-dreams-server` với entrypoint chạy được bằng `cargo run --bin ai-dreams-server`.
- [ ] `BE-00.3` Thêm config loading tối thiểu từ env và fallback values cho local development.
- [ ] `BE-00.4` Expose `health` hoặc `world stub` endpoint để frontend có target kết nối ban đầu.
- [ ] `BE-00.5` Thiết lập logging cơ bản đủ để đọc startup/config/runtime errors.
- [ ] `BE-00.6` Verify backend boot thành công trên local clean path không cần setup ngoài docs đã nêu.

## Frontend Checklist

- [ ] `FE-00.1` Tạo app React + Vite với commands chạy local rõ ràng.
- [ ] `FE-00.2` Tạo app shell có layout rỗng nhưng phản ánh đúng hướng product shell tương lai.
- [ ] `FE-00.3` Thiết lập API client stub và config base URL để nối được backend stub.
- [ ] `FE-00.4` Thêm loading, empty và error shell tối thiểu cho first-run experience.
- [ ] `FE-00.5` Chốt conventions cho routes, components, state và cấu trúc feature folder.
- [ ] `FE-00.6` Verify frontend boot được độc lập và chạy được cùng backend stub trong local flow.

## DevOps Checklist

- [ ] `DO-00.1` Tạo `scripts/dev.sh` hoặc local orchestration script để chạy backend/frontend theo một lệnh rõ ràng.
- [ ] `DO-00.2` Tạo `.env.example` với mô tả biến tối thiểu cho cả backend và frontend.
- [ ] `DO-00.3` Thêm scripts build/lint/check cơ bản cho hai app shells.
- [ ] `DO-00.4` Thiết lập CI tối thiểu để verify backend build và frontend build không hỏng.
- [ ] `DO-00.5` Chuẩn hóa commands local dev trong docs và script names cho thống nhất.
- [ ] `DO-00.6` Verify contributor path từ repo trống tới first run bằng đúng docs hiện hành.

## Demo & Sign-off

- Demo backend stub running.
- Demo frontend shell running.
- Demo local dev flow từ clone tới first run.
- [ ] Acceptance criteria được review đủ.
- [ ] Carry-over items được ghi lại sang Sprint 01 hoặc `MASTER-BACKLOG.md`.
- [ ] README và DEV-SETUP đã cập nhật theo trạng thái runnable thật.
- Sign-off owners: Tech lead + project lead.
