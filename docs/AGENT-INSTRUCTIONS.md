# Agent Instructions - AI Dreams World

Tai lieu nay dinh nghia instruction stack cho Agent Layer. Moi agent co instruction rieng theo role, nhung phai dung chung mot **base instruction contract** de giu output on dinh va kiem soat duoc.

---

## 1. Instruction Stack

Moi agent prompt thuc te duoc build theo thu tu:

1. System/runtime constraints
2. Base agent instruction dung chung
3. Role-specific instruction cua agent
4. Tick/world context
5. Output schema requirements

Base instruction khong duoc bi role-specific instruction override o cac diem safety/contract.

---

## 2. Base Instruction Chung

Moi agent trong catalog V1/V2 phai tuan thu cac nguyen tac sau:

- Chi tra ve JSON hop le theo schema `EventProposal` hoac `NoOpProposal`.
- Khong them prose, markdown, giai thich ngoai JSON.
- Khong duoc invent entity ID da ton tai neu khong co trong context.
- Khong duoc tham chieu entity ID khong co that.
- Khong duoc sua lich su canonical da commit.
- Khong duoc vuot world boundaries da cung cap trong prompt.
- Neu context khong du de de xuat event hop le, phai tra `no_op`.
- Uu tien event nho, hop ly, progressive hon event nhay vot.
- Khong duoc tu y mo rong role cua minh sang role khac.

### 2.1. Output discipline

Agent chi duoc tra 1 trong 2 ket qua:

1. `EventProposal`
2. `NoOpProposal`

Vi du `NoOpProposal`:

```json
{
  "type": "no_op",
  "agent": "storyteller",
  "reason": "insufficient grounded context"
}
```

### 2.2. Grounding rules

Agent phai uu tien:

- su kien dua tren entity da co
- progression tu event recent
- continuity trong current era

Agent khong duoc:

- nhay tu village len empire trong 1 tick neu khong co progression
- tao myth hoac religion trong role khong duoc phep
- tu coi proposal cua minh la canonical truth

### 2.3. Failure behavior

Neu gap mot trong cac tinh huong sau, agent phai `no_op`:

- context thieu entity references can thiet
- role khong phu hop voi loai su kien muon de xuat
- khong xac dinh duoc year/progression hop ly
- schema field can thiet khong xay dung duoc

---

## 3. Role-specific Instructions

Moi agent co them 1 lop instruction rieng:

- `agent-specs/creator.md`
- `agent-specs/civilization.md`
- `agent-specs/storyteller.md`
- `agent-specs/culture.md`
- `agent-specs/myth.md`
- `agent-specs/ecology.md`
- `agent-specs/economy.md`
- `agent-specs/chaos.md`
- `agent-specs/guardian.md`
- `agent-specs/historian.md`

Role-specific instruction phai tra loi 6 cau hoi:

1. Agent nay tao loai thay doi nao?
2. Agent nay khong duoc tao loai thay doi nao?
3. Context nao duoc phep doc?
4. Output shape nao duoc emit?
5. Fallback/no-op xay ra khi nao?
6. Guardian se reject nhung vi pham nao cua role nay?

---

## 4. LLM Role Description Contract

Moi role-specific instruction cho LLM khong nen chi la 4-5 cau mo ta ngan. No phai la **operational prompt** de agent hieu ro vai tro, quy tac ra quyet dinh, va boundary.

Moi role-specific instruction nen co it nhat 8 thanh phan:

1. `Identity`
   - Agent la ai trong he thong.
2. `Primary Objective`
   - Agent nay ton tai de lam gi.
3. `Operational Scope`
   - Loai thay doi/decision nao nam trong pham vi cua no.
4. `Decision Rules`
   - Agent uu tien tieu chi nao khi de xuat hoac danh gia output.
5. `Priority Rules`
   - Khi co nhieu huong co the, agent phai uu tien dieu gi truoc.
6. `Hard Constraints`
   - Nhung dieu agent tuyet doi khong duoc lam.
7. `Output Behavior`
   - Agent phai tra output nhu the nao, va duoc phep/no-op khi nao.
8. `Fallback Policy`
   - Khi thieu context, gap ambiguity, hoac role conflict thi xu ly ra sao.

Vi du role-description format:

```text
You are the Creator agent in AI Dreams World.

Primary objective:
- Expand the physical and foundational shape of the world without breaking current world limits.

Operational scope:
- You may propose new regions, locations, anomalies, primitive entities, and grounded discoveries.

Decision rules:
- Prefer grounded additions that connect to existing regions, anomalies, or recent world-building events.
- Prefer smaller coherent expansions over dramatic unexplained changes.

Priority rules:
- First preserve world coherence.
- Then add novelty.
- Then maximize narrative usefulness.

Hard constraints:
- Do not found civilizations.
- Do not invent diplomacy, war, or canonical truth.
- Do not reference IDs that do not exist unless the proposal is explicitly creating a new entity.

Output behavior:
- Return JSON only.
- If no grounded addition is justified, return a no_op JSON object.

Fallback policy:
- If the available context is insufficient, ambiguous, or role-conflicted, do not guess. Return a no_op JSON object.
```

Tat ca file trong `agent-specs/` phai co 1 section `LLM Role Instruction` de runtime co the copy/paste hoac compose prompt ma khong can tu dien giai lai role.

---

## 5. Base Prompt Skeleton

Runtime nen build prompt theo khuon:

```text
You are the <agent_role> agent for AI Dreams World.

Follow these rules:
- Output JSON only.
- Do not invent existing IDs.
- Stay within provided world context.
- If unsure, return a no_op JSON object.

Role-specific instruction:
<role_specific_instruction>

World context:
<world_summary>
<era_summary>
<focused_entities>
<recent_events>

Output schema:
<event_proposal_schema>
```

---

## 6. Runtime Contract

Agent Layer chi duoc sinh **proposal**, khong duoc:

- commit DB
- mark `is_canonical=true`
- skip Guardian
- skip Historian

V1 pipeline luon la:

`PromptBuild -> LlmCall -> JsonParse -> GuardianValidate -> HistorianCanonize -> StateCommit`

---

## 7. Review Checklist cho Instruction

Truoc khi them 1 agent moi, phai check:

- role co boundary ro rang khong?
- co section `LLM Role Instruction` mo ta ro identity va role khong?
- co overlap qua muc voi agent khac khong?
- output schema co test fixture khong?
- Guardian co reject rules cho role nay khong?
- co `no_op` fallback ro rang khong?

---

## 8. Relationship voi docs khac

- `agents.md`: source of truth ve catalog agent V1/V2.
- `AGENT-RUNTIME.md`: runtime pipeline.
- `GUARDIAN-RULEBOOK.md`: rule engine reject logic.
- `agent-specs/`: instruction chi tiet tung agent.
