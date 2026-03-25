# Sprint 12 – Task Breakdown

## Breakdown Goal

Tạo multi-world foundation ở tầng data/runtime để các sprint 13–14 chỉ productize UX thay vì phải sửa core assumptions.

## Work Packages

- `WP1` World metadata and indirection
- `WP2` Snapshot/fork hooks
- `WP3` Recovery and multi-world ops

## Atomic Tasks

| ID | Parent | Stream | Task | Depends On | Output |
| --- | --- | --- | --- | --- | --- |
| T12-01 | ADW-S12-BA-01 | BA | Chốt world metadata schema, current-world semantics và snapshot provenance baseline | None | multi-world contract |
| T12-02 | ADW-S12-BE-01 | Backend | Add world registry và current-world indirection trong core flows | T12-01 | world registry |
| T12-03 | ADW-S12-BE-01 | Backend | Separate world metadata khỏi world state ở nơi cần thiết | T12-02 | metadata/state separation |
| T12-04 | ADW-S12-BE-01 | Backend | Add snapshot/fork hooks baseline chưa gắn final UX semantics | T12-01,T12-03 | snapshot/fork hooks |
| T12-05 | ADW-S12-BE-01 | Backend | Remove hard-coded single-world assumptions khỏi generation, feed, export và config paths | T12-02,T12-04 | multi-world safe core |
| T12-06 | ADW-S12-FE-01 | Frontend | Build minimal current-world selector/list shell | T12-02 | selector shell |
| T12-07 | ADW-S12-DO-01 | DevOps | Implement backup/restore flows cho multiple worlds | T12-03,T12-04 | multi-world recovery path |
| T12-08 | ADW-S12-DO-01 | DevOps | Add world growth monitoring labels và run recovery drill cho snapshot metadata path | T12-07 | recovery drill note |

## Suggested Sequence

1. `T12-01`
2. `T12-02 -> T12-03 -> T12-04`
3. `T12-05`
4. `T12-06`
5. `T12-07 -> T12-08`

## Cut Line

- Must-have: `T12-01..T12-07`
- Can defer: `T12-08` observability/runbook depth

## Verification Artifacts

- Current-world UX cũ vẫn hoạt động
- Multi-world metadata survive restart/reload
- Core flows không còn assumption kiểu single world forever
