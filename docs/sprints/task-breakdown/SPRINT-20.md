# Sprint 20 – Task Breakdown

## Breakdown Goal

Chốt documented vision bằng collaborative viewing session-based, có shared observation và controlled interventions thay vì trôi thành multiplayer platform.

## Work Packages

- `WP1` Session model and synchronization
- `WP2` Permission-aware collaborative UX
- `WP3` Abuse, moderation and scale controls

## Atomic Tasks

| ID | Parent | Stream | Task | Depends On | Output |
| --- | --- | --- | --- | --- | --- |
| T20-01 | ADW-S20-BA-01 | BA | Chốt session role/permission model, audit schema và conflict-resolution semantics | None | collaboration contract |
| T20-02 | ADW-S20-BE-01 | Backend | Add session model và world-session binding | T19-04,T20-01 | session persistence |
| T20-03 | ADW-S20-BE-01 | Backend | Sync shared observation state across viewers | T20-02 | shared session state |
| T20-04 | ADW-S20-BE-01 | Backend | Enforce permission checks trên intervention path và record all session actions | T20-02,T20-03 | permission + audit layer |
| T20-05 | ADW-S20-BE-01 | Backend | Handle concurrent actions deterministically | T20-04 | conflict-safe runtime |
| T20-06 | ADW-S20-FE-01 | Frontend | Build join/view shared session flow | T20-02,T20-03 | session join UI |
| T20-07 | ADW-S20-FE-01 | Frontend | Build presence và shared session state surfaces | T20-03,T20-06 | presence UI |
| T20-08 | ADW-S20-FE-01 | Frontend | Build permission-aware intervention controls | T20-04,T20-07 | role-aware control UI |
| T20-09 | ADW-S20-FE-01 | Frontend | Build conflict, reconnect và error UX | T20-05,T20-07 | resilient session UX |
| T20-10 | ADW-S20-DO-01 | DevOps | Add rate limits, abuse mitigations và multi-viewer load tests | T20-05,T20-09 | collaboration hardening |
| T20-11 | ADW-S20-DO-01 | DevOps | Prepare kill-switch và moderation runbook | T20-10 | moderation/kill-switch pack |

## Suggested Sequence

1. `T20-01`
2. `T20-02 -> T20-03 -> T20-04 -> T20-05`
3. `T20-06 -> T20-07 -> T20-08 -> T20-09`
4. `T20-10 -> T20-11`

## Cut Line

- Must-have: `T20-01..T20-10`
- Can defer: `T20-11` runbook polish

## Verification Artifacts

- 2+ users thấy consistent shared world session
- Unauthorized controls vừa hidden vừa blocked
- Audit trail đủ cho support và moderation
