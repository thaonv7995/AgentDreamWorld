# API Contract - AI Dreams World

Tai lieu nay chot contract API V1 de frontend, backend, test harness, va export layer cung dung chung mot nguon tham chieu.

---

## 1. Scope V1

V1 chi cam ket 5 endpoint:

- `GET /worlds/current`
- `GET /worlds/current/events`
- `POST /worlds/current/tick`
- `POST /worlds/current/export/wiki`
- `POST /worlds/current/export/annals`

Moi endpoint deu tra JSON va phai tuan theo response envelope thong nhat.

---

## 2. API Conventions

### 2.1. Response envelope bat buoc

Moi response JSON V1 phai co 4 field core:

```json
{
  "success": true,
  "code": "0000",
  "message": "Dashboard data retrieved successfully",
  "data": {}
}
```

Quy uoc:

- `success`: boolean.
- `code`: chuoi 4 chu so, vi du `0000`, `1001`, `4002`.
- `message`: human-readable message ngan, on dinh, de frontend hien thi/log.
- `data`: object, array, hoac `null`.

### 2.2. Optional fields

V1 cho phep them cac field sau khi can:

- `meta`: paging, filters, totals, file info.
- `errors`: danh sach validation details.
- `trace_id`: correlation id cho debug.

Vi du list response:

```json
{
  "success": true,
  "code": "0000",
  "message": "Events retrieved successfully",
  "data": [],
  "meta": {
    "page": 1,
    "page_size": 20,
    "total": 120,
    "filters": {
      "civilization_id": "civ_01"
    }
  }
}
```

Vi du error response:

```json
{
  "success": false,
  "code": "1001",
  "message": "Invalid request parameters",
  "data": null,
  "errors": [
    {
      "field": "from_year",
      "reason": "must be less than or equal to to_year"
    }
  ]
}
```

### 2.3. HTTP status mapping

- `2xx`: request thanh cong, `success=true`.
- `4xx`: request khong hop le, khong thuc hien duoc, `success=false`.
- `5xx`: loi he thong/provider/storage, `success=false`.

Business `code` khong thay the HTTP status. Frontend phai doc ca hai:

- HTTP status de phan loai protocol-level outcome.
- `code` de xu ly nghiep vu/on dinh theo contract.

### 2.4. Content type

- Request body JSON: `Content-Type: application/json`
- Response JSON: `Content-Type: application/json; charset=utf-8`

### 2.5. Timestamps va IDs

- Date/time dung ISO-8601 UTC, vi du `2026-03-25T10:30:00Z`.
- World years trong simulation la integer `year`.
- IDs dung string on dinh, lower_snake_case hoac prefix form:
  - `world_main`
  - `reg_01`
  - `civ_03`
  - `set_07`
  - `evt_000123`

### 2.6. Pagination

List endpoint V1 dung pagination query params:

- `page`: default `1`
- `page_size`: default `20`, max `100`

Neu endpoint khong paged o implementation dau tien, van nen giu `meta` shape de khong pha contract sau nay.

### 2.7. Filtering

Filter params khong hop le phai tra:

- HTTP `400`
- `code: "1001"`
- `data: null`

Khong silently ignore filter sai.

---

## 3. Endpoint Contracts

## 3.1. `GET /worlds/current`

Muc dich:

- Lay summary world hien tai cho `World Overview`.

### Success

- HTTP `200`
- `code: "0000"`

```json
{
  "success": true,
  "code": "0000",
  "message": "World summary retrieved successfully",
  "data": {
    "world_id": "world_main",
    "name": "The Glass Delta",
    "current_year": 245,
    "current_era": {
      "era_id": "era_02",
      "name": "Age of Tidal Cities"
    },
    "stats": {
      "regions": 4,
      "civilizations": 5,
      "settlements": 14,
      "canonical_events": 86
    },
    "highlights": [
      "Three coastal settlements formed a trade pact.",
      "The northern ruins were rediscovered."
    ]
  }
}
```

### Failure cases

- `5004` internal server error
- `5001` database read failure

---

## 3.2. `GET /worlds/current/events`

Muc dich:

- Lay events cho ca Dream Feed va Timeline View.
- Dream Feed render `title` + `summary` + `tags`.
- Timeline View co the chi render `year` + `title` + `is_canonical`.

### Query params

- `page`
- `page_size`
- `from_year`
- `to_year`
- `type`
- `agent`
- `civilization_id`
- `canonical_only`

### Rules

- `from_year <= to_year`
- `page >= 1`
- `1 <= page_size <= 100`
- `type` va `agent` phai nam trong enum hop le cua he thong

### Success

- HTTP `200`
- `code: "0000"`

```json
{
  "success": true,
  "code": "0000",
  "message": "Events retrieved successfully",
  "data": [
    {
      "event_id": "evt_000123",
      "year": 245,
      "title": "The River Grain Pact",
      "event_type": "trade",
      "agent": "civilization",
      "summary": "Three river ports opened a shared grain route after a harsh winter, easing famine fears across the lower basin.",
      "description": "The river ports formed a shared grain route.",
      "tags": ["trade", "grain", "river-basin"],
      "affected_entities": {
        "civilization_ids": ["civ_02", "civ_04"],
        "region_ids": ["reg_03"]
      },
      "is_canonical": true
    }
  ],
  "meta": {
    "page": 1,
    "page_size": 20,
    "total": 1,
    "filters": {
      "from_year": 200,
      "to_year": 300,
      "canonical_only": true
    }
  }
}
```

### Field notes

- `title`: ngan, de dung cho marker tren timeline va tieu de Dream Feed card
- `summary`: 1-2 cau ngan, factual-narrative, de Dream Feed khong bien thanh event log kho khan
- `description`: optional detail line neu can detail view
- `tags`: nhom tu khoa de filter/hien thi card meta

### Failure cases

- HTTP `400`, `1001` invalid query params
- HTTP `400`, `1003` unsupported filter value
- HTTP `500`, `5001` database read failure

---

## 3.3. `POST /worlds/current/tick`

Muc dich:

- Trigger 1 tick thu cong cho dev/debug/test.

### Request body

V1 cho phep body rong hoac body toi thieu:

```json
{
  "trigger": "manual",
  "trace_label": "dev-debug"
}
```

Field rules:

- `trigger`: optional, default `manual`
- `trace_label`: optional string ngan de log/debug

### Success

- HTTP `200`
- `code: "0000"`

```json
{
  "success": true,
  "code": "0000",
  "message": "Tick completed successfully",
  "data": {
    "tick_id": "tick_000045",
    "world_id": "world_main",
    "year_before": 240,
    "year_after": 245,
    "agents_selected": ["creator", "storyteller"],
    "proposals_generated": 2,
    "proposals_accepted": 1,
    "proposals_rejected": 1,
    "canonical_events_created": ["evt_000123"]
  }
}
```

### Failure cases

- HTTP `409`, `3002` tick already in progress
- HTTP `409`, `3003` simulation disabled in current process mode
- HTTP `422`, `3001` tick rejected by world/runtime constraints
- HTTP `502`, `4004` provider timeout
- HTTP `502`, `4005` provider unavailable
- HTTP `500`, `5001` database write failure

---

## 3.4. `POST /worlds/current/export/wiki`

Muc dich:

- Tao wiki-style export tu world canonical state.

### Request body

V1 body co the rong:

```json
{}
```

### Success

- HTTP `200`
- `code: "0000"`

```json
{
  "success": true,
  "code": "0000",
  "message": "Wiki export completed successfully",
  "data": {
    "world_id": "world_main",
    "format": "wiki",
    "file_path": "exports/world_main/wiki.md",
    "exported_at": "2026-03-25T10:30:00Z"
  }
}
```

### Failure cases

- HTTP `500`, `5002` export failed
- HTTP `500`, `5003` storage unavailable

---

## 3.5. `POST /worlds/current/export/annals`

Muc dich:

- Tao annals/chronicle export tu canonical timeline.

### Success

- HTTP `200`
- `code: "0000"`

```json
{
  "success": true,
  "code": "0000",
  "message": "Annals export completed successfully",
  "data": {
    "world_id": "world_main",
    "format": "annals",
    "file_path": "exports/world_main/annals.md",
    "exported_at": "2026-03-25T10:35:00Z"
  }
}
```

### Failure cases

- HTTP `500`, `5002` export failed
- HTTP `500`, `5003` storage unavailable

---

## 4. Validation Error Shape

Khi request validation fail, dung `errors` array:

```json
{
  "success": false,
  "code": "1001",
  "message": "Invalid request parameters",
  "data": null,
  "errors": [
    {
      "field": "page_size",
      "reason": "must be between 1 and 100"
    },
    {
      "field": "type",
      "reason": "unsupported event type"
    }
  ]
}
```

V1 khong can nested error object phuc tap hon.

---

## 5. Implementation Rules

- Backend phai dung mot response builder chung de khong drift envelope.
- Frontend khong duoc parse response theo ad-hoc shape tung endpoint.
- API contract tests phai verify:
  - du 4 field core
  - `code` luon la string 4 chu so
  - `data` khong duoc bo qua
- Log/trace layer nen luu ca HTTP status va business `code`.

---

## 6. Relationship voi docs khac

- `API-CODES.md`: bang business codes chi tiet.
- `MVP-SPEC.md`: pham vi endpoint V1.
- `AGENT-RUNTIME.md`: runtime behavior cho `POST /tick`.
- `TEST-AND-EVAL-STRATEGY.md`: contract tests va replay tests.
