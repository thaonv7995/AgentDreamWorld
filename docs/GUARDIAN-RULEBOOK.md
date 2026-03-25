# Guardian Rulebook - AI Dreams World

Guardian la lop validation bat buoc giua imagination layer va canonical world state. Tai lieu nay bien Guardian tu mot y tuong thanh mot **rule catalog** co the implement, test, va trace.

---

## 1. Vai tro cua Guardian

Guardian khong sang tao noi dung moi. Guardian chi:

- validate schema/progression/reference
- reject proposal khong hop le
- gan reject reason co cau truc
- chuyen proposal hop le sang Historian/World Model

Guardian la "gate", khong phai "author".

---

## 2. Vi tri trong pipeline

Pipeline V1:

`PromptBuild -> LlmCall -> JsonParse -> GuardianValidate -> HistorianCanonize -> StateCommit`

Neu Guardian reject:

- khong duoc commit DB
- khong duoc historian canonicalize event do
- tick log phai luu `rule_id`, `code`, `reason`

---

## 3. Violation Shape

Moi vi pham nen map ve 1 object co cau truc:

```json
{
  "rule_id": "GR-004",
  "code": "4002",
  "severity": "error",
  "message": "Proposal references a non-existent civilization_id",
  "action": "reject"
}
```

Quy uoc:

- `rule_id`: ID cua rule trong rulebook
- `code`: business code API, thuong la `4002`
- `severity`: `error` hoac `warning`
- `action`: `reject`, `downgrade_to_no_op`, hoac `allow_with_warning`

V1 nen rat chat:

- rule `error` => reject
- `warning` chi dung cho van de mo ta/co the normalize, khong dung cho state-changing fact

---

## 4. Rule Groups

## 4.1. Schema validity

| Rule ID | Ten rule | Action |
| --- | --- | --- |
| `GR-001` | Event type khong hop le | `reject` |
| `GR-002` | Thieu field bat buoc | `reject` |
| `GR-003` | `affected_entities` sai shape/schema | `reject` |

Mo ta:

- Proposal phai map duoc sang `EventProposal` hop le.
- Guardian khong sua schema thay agent; schema sai la reject.

## 4.2. Entity reference validity

| Rule ID | Ten rule | Action |
| --- | --- | --- |
| `GR-004` | Tham chieu entity ID khong ton tai | `reject` |
| `GR-005` | Relation giua cac entity khong hop le trong domain | `reject` |

Vi du:

- `civilization_id` khong co trong DB/context
- settlement thuoc region khac voi region event dang claim

## 4.3. Chronology va progression

| Rule ID | Ten rule | Action |
| --- | --- | --- |
| `GR-006` | Year/progression khong hop le | `reject` |
| `GR-007` | Leap progression vuot muc cho phep | `reject` |
| `GR-008` | Event mau thuan voi canonical state moi nhat | `reject` |

Vi du:

- village -> empire trong 1 tick, khong co chuoi progression
- event claim mot civilization "founded" du da ton tai tu truoc

## 4.4. Duplicate va novelty control

| Rule ID | Ten rule | Action |
| --- | --- | --- |
| `GR-009` | Duplicate exact event | `reject` |
| `GR-010` | Near-duplicate event trong recent window | `reject` |

Vi du:

- cung description, cung event type, cung entities, cung nam
- 2 trade-route events chi khac wording nhung trung tac dong trong 1 tick window

## 4.5. Role boundary enforcement

| Rule ID | Ten rule | Action |
| --- | --- | --- |
| `GR-011` | Agent tao event ngoai role cua minh | `reject` |
| `GR-012` | Agent tu nhan canonical authority | `reject` |

Vi du:

- `Storyteller` tao mot `creation` event sinh region moi
- proposal co field/claim `is_canonical=true`

## 4.6. World size va simulation caps

| Rule ID | Ten rule | Action |
| --- | --- | --- |
| `GR-013` | Vuot world size cap V1 | `reject` |
| `GR-014` | Vuot tick cap V1 | `reject` |

Caps V1 can bao ve:

- 1 world
- 3-4 regions
- 3-6 civilizations
- <= 20 settlements
- 1 major event + toi da 2 minor events/tick

## 4.7. Export/canonical safety

| Rule ID | Ten rule | Action |
| --- | --- | --- |
| `GR-015` | Proposal co gang sua event canonical da ton tai | `reject` |
| `GR-016` | Proposal khong map duoc sang canonical event model | `reject` |

---

## 5. Warning Rules

Warning chi dung cho cac truong hop khong thay doi fact:

| Rule ID | Ten rule | Action |
| --- | --- | --- |
| `GW-001` | Description qua dai, can normalize | `allow_with_warning` |
| `GW-002` | Tag/phu tro thieu, nhung core fact hop le | `allow_with_warning` |

Neu team muon Giam do phuc tap V1, co the chon implementation don gian hon:

- tat ca warning deu duoc historian normalize sau
- Guardian chi reject/error, khong mutate content

---

## 6. Rule-to-Code Mapping

Mapping business code de dung o API/log:

- Parse fail truoc khi vao Guardian -> `4001`
- Guardian reject do rulebook -> `4002`
- Rule config file bi loi -> `4007`

Mapping phan loai:

- request sai input API -> `1001`
- proposal sai runtime/Guardian -> `4002`
- commit DB fail sau khi qua Guardian -> `5001`

---

## 7. Decision Policy

Guardian nen uu tien:

1. reference validity
2. chronology/progression
3. role boundary
4. duplicate control
5. descriptive quality

Neu 1 proposal vi pham nhieu rule:

- log rule nghiem trong nhat dau tien
- co the luu them `all_rule_ids` trong tick log cho debug

---

## 8. Test Requirements

Moi rule `GR-*` phai co it nhat:

- 1 fixture pass
- 1 fixture fail

Nhom toi thieu can co:

- invalid entity ref
- impossible progression
- duplicate event
- role/event mismatch
- world cap exceeded

---

## 9. Relationship voi docs khac

- `AGENT-RUNTIME.md`: vi tri Guardian trong pipeline.
- `API-CODES.md`: map `4002`, `4007`.
- `agent-specs/*.md`: boundary theo tung role.
- `TEST-AND-EVAL-STRATEGY.md`: fixture va replay tests cho Guardian.
