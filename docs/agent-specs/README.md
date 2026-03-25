# Agent Specs - AI Dreams World

Thu muc nay chua instruction/contract chi tiet cho day du **10 agent** trong catalog cua du an.

---

## Agent catalog

### V1 core runtime

- `creator.md`
- `civilization.md`
- `storyteller.md`
- `guardian.md`
- `historian.md`

### V2 expansion agents

- `culture.md`
- `myth.md`
- `ecology.md`
- `economy.md`
- `chaos.md`

---

## Format chung cua moi agent spec

Moi file trong thu muc nay phai mo ta:

- mission
- LLM role instruction
- khi nao agent duoc chon
- duoc phep tao thay doi nao
- khong duoc lam gi
- context duoc doc
- output contract
- fallback/no-op behavior
- Guardian reject points lien quan

---

## Relationship voi docs khac

- `../agents.md`: source of truth ve agent catalog.
- `../AGENT-INSTRUCTIONS.md`: base instruction stack.
- `../GUARDIAN-RULEBOOK.md`: boundary enforcement.
