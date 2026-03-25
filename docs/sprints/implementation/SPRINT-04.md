# Sprint 04 – Implementation Companion

## Implementation Intent

Sprint 04 biến vertical slice thành **observer experience**. Không thêm world logic mới nếu không trực tiếp phục vụ Dream Feed và World Overview.

## Build Slices

- Dream Feed UI.
- World Overview UI.
- Polling/refresh flow.
- Query optimization vừa đủ cho observer path.

## Backend Implementation

- Optimize read models cho feed/overview.
- Add filters/indexes/queries cần cho observer flow.
- Không mở rộng schema nếu projection hiện tại đủ dùng.

## Frontend Implementation

- Feed cards, filters, refresh states.
- Overview panels cho regions/civilizations/settlements/basic stats.
- Strong loading, empty, stale, retry states.

## DevOps / Quality

- Preview build path cho demo.
- Visual smoke checks cho shell and API integration.
- Verify current-world startup path ổn định.

## Contracts To Freeze

- Feed filter semantics.
- Overview information hierarchy.
- Poll/refresh behavior expectations.

## Verification

- User mở app thấy world data thật.
- Feed refresh không double-count events.
- Overview numbers khớp với backend summary.

## Handoff To Sprint 05

- Timeline and control surfaces phải gắn vào observer shell hiện tại, không tạo app shell mới.
- Read models ở sprint này là nền cho timeline projections.
