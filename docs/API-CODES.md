# API Codes - AI Dreams World

Tai lieu nay dinh nghia business response code dung chung cho API V1. Tat ca `code` deu la **chuoi 4 chu so**.

---

## 1. Coding Rules

- `0000` la success chung.
- `1xxx` cho request/validation.
- `2xxx` cho world/domain lookup.
- `3xxx` cho simulation/tick control.
- `4xxx` cho agent runtime/LLM/Guardian/Historian.
- `5xxx` cho export/storage/internal system.

Quy uoc:

- Cung mot tinh huong nghiep vu phai map cung mot code.
- Khong dung message de thay cho code.
- HTTP status va `code` phai duoc map nhat quan.

---

## 2. Code Table

| Code | Name | HTTP status thuong dung | Nghia |
| --- | --- | --- | --- |
| `0000` | SUCCESS | `200` | Thanh cong chung |
| `1000` | BAD_REQUEST | `400` | Request khong hop le o muc tong quat |
| `1001` | INVALID_PARAMETERS | `400` | Query/body params sai format hoac sai quan he |
| `1002` | MISSING_REQUIRED_FIELD | `400` | Thieu field bat buoc |
| `1003` | UNSUPPORTED_FILTER | `400` | Filter/query value khong duoc ho tro |
| `1004` | INVALID_PAGINATION | `400` | `page`/`page_size` khong hop le |
| `1005` | MALFORMED_JSON_BODY | `400` | Request body JSON khong parse duoc |
| `1006` | UNSUPPORTED_CONTENT_TYPE | `415` | Content type khong duoc ho tro |
| `2000` | DOMAIN_ERROR | `404` | Loi domain chung |
| `2001` | WORLD_NOT_FOUND | `404` | Khong tim thay world |
| `2002` | REGION_NOT_FOUND | `404` | Khong tim thay region |
| `2003` | CIVILIZATION_NOT_FOUND | `404` | Khong tim thay civilization |
| `2004` | SETTLEMENT_NOT_FOUND | `404` | Khong tim thay settlement |
| `2005` | EVENT_NOT_FOUND | `404` | Khong tim thay event |
| `2006` | ENTITY_REFERENCE_INVALID | `422` | Entity ref hop le ve format nhung khong hop le ve domain |
| `3000` | SIMULATION_ERROR | `409` | Loi simulation chung |
| `3001` | TICK_REJECTED | `422` | Tick khong the commit do runtime/world constraints |
| `3002` | TICK_ALREADY_IN_PROGRESS | `409` | Dang co tick khac chay |
| `3003` | SIMULATION_DISABLED | `409` | Process mode hien tai khong cho tick |
| `3004` | WORLD_LOCKED | `409` | World tam thoi khong cho mutation |
| `3005` | TICK_RATE_LIMITED | `429` | Tick bi gioi han tan suat |
| `4000` | AGENT_RUNTIME_ERROR | `502` | Loi runtime chung o tang agent |
| `4001` | AGENT_OUTPUT_PARSE_FAILED | `502` | Output LLM khong parse/schema-map duoc |
| `4002` | GUARDIAN_VALIDATION_FAILED | `422` | Proposal bi Guardian reject |
| `4003` | HISTORIAN_CANONIZATION_FAILED | `500` | Historian khong canonicalize duoc ket qua hop le |
| `4004` | LLM_PROVIDER_TIMEOUT | `502` | Provider timeout |
| `4005` | LLM_PROVIDER_UNAVAILABLE | `502` | Provider unavailable/upstream error |
| `4006` | UNSUPPORTED_AGENT_ROLE | `500` | Role agent khong hop le voi runtime config |
| `4007` | RULE_CONFIGURATION_ERROR | `500` | Rule file/rule engine config loi |
| `5000` | SYSTEM_ERROR | `500` | Loi he thong chung |
| `5001` | DATABASE_OPERATION_FAILED | `500` | Doc/ghi DB that bai |
| `5002` | EXPORT_FAILED | `500` | Export khong tao duoc artifact |
| `5003` | STORAGE_UNAVAILABLE | `500` | Disk/path/storage layer khong san sang |
| `5004` | INTERNAL_SERVER_ERROR | `500` | Exception chung chua classify duoc |

---

## 3. Recommended Mappings

### 3.1. API layer

- Param sai -> `1001`
- Body JSON hong -> `1005`
- Content type sai -> `1006`

### 3.2. Query/domain layer

- Filter civilization khong ton tai -> `2003`
- Filter event khong ton tai -> `2005`
- Ref toi entity khong hop le trong domain -> `2006`

### 3.3. Simulation layer

- Tick bi chan do process mode -> `3003`
- Tick chay trung -> `3002`
- Tick vi pham world constraints -> `3001`

### 3.4. Agent layer

- LLM tra ve text khong parse duoc -> `4001`
- Guardian reject proposal -> `4002`
- Provider timeout -> `4004`
- Provider loi upstream -> `4005`

### 3.5. System layer

- SQLite query/commit fail -> `5001`
- Export markdown file fail -> `5002`
- Exception chua classify -> `5004`

---

## 4. Usage Examples

### 4.1. Validation error

```json
{
  "success": false,
  "code": "1001",
  "message": "Invalid request parameters",
  "data": null
}
```

### 4.2. Guardian reject

```json
{
  "success": false,
  "code": "4002",
  "message": "Guardian rejected the proposal",
  "data": null
}
```

### 4.3. Tick conflict

```json
{
  "success": false,
  "code": "3002",
  "message": "A tick is already in progress",
  "data": null
}
```

---

## 5. Relationship voi docs khac

- `API-CONTRACT.md`: envelope va endpoint shapes.
- `GUARDIAN-RULEBOOK.md`: rule-level reject catalog phia sau `4002`.
- `AGENT-RUNTIME.md`: source of truth cho runtime stages.
