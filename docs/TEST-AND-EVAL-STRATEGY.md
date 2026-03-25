# Test and Eval Strategy - AI Dreams World

He thong nay co limitation lon: output loi qua nhieu stage non-deterministic cua LLM pipeline. Tai lieu nay chot cach test de team van co the ship V1 ma khong "bay mu".

---

## 1. Muc tieu

Muc tieu cua test/eval strategy V1:

- test duoc ma khong can goi LLM that o moi lan CI
- replay duoc tick sequence quan trong
- phan loai ro bug nam o stage nao
- giu API shape on dinh cho frontend
- phat hien regression ve coherence/progression som

---

## 2. Testing Pyramid cho V1

## 2.1. Unit tests

Unit tests cho logic xac dinh va re:

- request validation
- response builder envelope
- query filter parsing
- prompt builder
- JSON parser/schema mapper
- Guardian rule evaluators
- Historian scoring/canonicalization heuristics
- projection builders cho world summary va event list

## 2.2. Fixture-based pipeline tests

Dung `MockAgentModel` de chay pipeline that ma khong goi provider:

`PromptBuild -> MockReply -> JsonParse -> Guardian -> Historian -> StateCommit`

Fixture nen nam o cau truc:

```text
fixtures/agents/
  creator/
  civilization/
  storyteller/
  guardian/
  historian/
```

Moi fixture nen co:

- `prompt_context.json`
- `llm_response.json` hoac `llm_response.txt`
- `expected_result.json`
- `expected_world_delta.json` khi can

## 2.3. Snapshot/replay tests

Can co bo test:

- seed world state ban dau
- chay `N` tick bang mock fixtures
- dump world state
- compare voi golden snapshot

Dung de bat:

- drift trong progression
- thay doi unintended o canonical event order
- bug trong projection builders

## 2.4. API contract tests

Moi endpoint V1 can verify:

- du 4 field core: `success`, `code`, `message`, `data`
- `code` luon la string 4 chu so
- HTTP status map dung voi business code
- shape `meta` on dinh neu co paging

## 2.5. Live smoke tests

Khong chay tren moi CI full run. Chi chay:

- nightly
- truoc release MVP
- hoac bang tay khi doi provider/model

Muc dich:

- xac nhan provider con hoat dong
- xac nhan prompt va schema van parse duoc
- thu thap mau output that de cap nhat fixtures

---

## 3. Error Classification theo Stage

Moi test/report phai gan bug vao 1 stage:

- `PromptBuild`
- `LlmCall`
- `JsonParse`
- `GuardianValidate`
- `HistorianCanonize`
- `StateCommit`

Neu khong phan loai theo stage, team se mat rat nhieu thoi gian debug sai lop.

---

## 4. Eval Rubric cho Event Quality

Voi fixture test hoac live sample review, danh gia moi proposal/canonical event theo 5 tieu chi:

| Tieu chi | Cau hoi | Score |
| --- | --- | --- |
| Reference validity | Entity refs co that va dung quan he khong? | `0-2` |
| Progression plausibility | Event co hop ly voi current era/recent events khong? | `0-2` |
| Role correctness | Agent co dung boundary role khong? | `0-2` |
| Canonical usefulness | Event co dang de dua vao timeline/feed khong? | `0-2` |
| Novelty without chaos | Event co moi nhung khong vo logic khong? | `0-2` |

Tong score:

- `8-10`: good
- `6-7`: usable but review
- `<=5`: fixture/problem can xu ly

Rubric nay dung cho:

- danh gia fixture moi
- review output that
- compare model/provider

---

## 5. Regression Gates

Truoc khi merge thay doi runtime/API/Guardian rules, can qua 4 gate:

1. Unit tests pass
2. API contract tests pass
3. Fixture pipeline tests pass
4. Snapshot replay khong drift, hoac drift da duoc giai thich/approve

Neu doi provider/model:

5. Live smoke test pass tren tap prompt mau toi thieu

---

## 6. Suggested Test Matrix

| Lop test | Moi commit | CI PR | Nightly | Release |
| --- | --- | --- | --- | --- |
| Unit tests | Co | Co | Co | Co |
| API contract tests | Co | Co | Co | Co |
| Fixture pipeline tests | Co | Co | Co | Co |
| Snapshot replay tests | Tuỳ scope | Co | Co | Co |
| Live provider smoke tests | Khong | Tuỳ scope | Co | Co |
| Export end-to-end tests | Tuỳ scope | Co | Co | Co |

---

## 7. Test Data Strategy

Can co 3 lop du lieu test:

### 7.1. Happy path fixtures

- creator sinh region hop le
- civilization lap settlement hop le
- storyteller tao discovery/trade/festival hop le

### 7.2. Reject fixtures

- invalid entity ref
- wrong event type for role
- impossible progression
- duplicate event
- malformed JSON

### 7.3. Long-run replay fixtures

- 5 tick genesis
- 10 tick civ growth
- 10 tick mixed narrative

Muc tieu la chay replay ngan nhung co y nghia, khong can mo phong hang tram tick trong CI.

---

## 8. Manual Review Protocol

Voi cac thay doi prompt/rule/model, review tay toi thieu 20 sample output:

- 5 creator
- 5 civilization
- 5 storyteller
- 5 edge/reject cases

Review questions:

- output co dung JSON schema khong?
- co hallucinate entity ID khong?
- co tao event qua lon so voi state hien tai khong?
- co sinh event lap lai khong?
- co de dua vao Dream Feed khong?

---

## 9. Deliverables can co tu Sprint 2-4

- `MockAgentModel`
- fixture library cho 3 creative agents
- Guardian rule tests
- API contract tests
- 1 lenh replay world state bang fixtures
- 1 lenh report reject reasons/latency/cost

---

## 10. Relationship voi docs khac

- `AGENT-RUNTIME.md`: pipeline stages va mock provider.
- `API-CONTRACT.md`: contract tests cho response shape.
- `GUARDIAN-RULEBOOK.md`: reject fixtures.
- `LIMITATIONS.md`: ly do phai uu tien replay/observability som.
