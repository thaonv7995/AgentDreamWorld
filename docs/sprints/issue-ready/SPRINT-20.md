# Sprint 20 – Issue-Ready Board

## Suggested Order

`EP-S20-01` -> `EP-S20-02` -> `EP-S20-03`

## Epic `EP-S20-01` – Session Model & Synchronization

- [ ] Epic complete

### Issue `ADW-S20-BA-01` – Collaboration contract

- [ ] Issue complete
- Depends on: `ADW-S19-BA-01`
- Subtasks:
  - [ ] `T20-01` Chốt session role/permission model, audit schema và conflict-resolution semantics

### Issue `ADW-S20-BE-01` – Shared session runtime

- [ ] Issue complete
- Depends on: `T19-04`, `T20-01`
- Subtasks:
  - [ ] `T20-02` Add session model và world-session binding
  - [ ] `T20-03` Sync shared observation state across viewers
  - [ ] `T20-04` Enforce permission checks trên intervention path và record all session actions
  - [ ] `T20-05` Handle concurrent actions deterministically

## Epic `EP-S20-02` – Permission-Aware Collaborative UX

- [ ] Epic complete

### Issue `ADW-S20-FE-01` – Collaborative session UI

- [ ] Issue complete
- Depends on: `T20-02`, `T20-03`, `T20-04`, `T20-05`
- Subtasks:
  - [ ] `T20-06` Build join/view shared session flow
  - [ ] `T20-07` Build presence và shared session state surfaces
  - [ ] `T20-08` Build permission-aware intervention controls
  - [ ] `T20-09` Build conflict, reconnect và error UX

## Epic `EP-S20-03` – Abuse, Moderation & Scale Controls

- [ ] Epic complete

### Issue `ADW-S20-DO-01` – Collaboration hardening

- [ ] Issue complete
- Depends on: `T20-05`, `T20-09`
- Subtasks:
  - [ ] `T20-10` Add rate limits, abuse mitigations và multi-viewer load tests
  - [ ] `T20-11` Prepare kill-switch và moderation runbook

## Verification Checklist

- [ ] 2+ users thấy consistent shared world session
- [ ] Unauthorized controls vừa hidden vừa blocked
- [ ] Audit trail đủ cho support và moderation
