# Worked example · archive a project

This fictional example follows one change through requirements, code analysis, review, and refresh. The named paths and task are illustrative. The focused scenarios can be exercised with a small in-memory fixture.

## 1. Intake and reconcile the request

Task `WORK-42` asks workspace administrators to archive a project. It must disappear from the active list and board, and remain available in history. An existing decision, `D-08`, treats history exports as historical access.

- `AC-archive-1` — an authorized admin can archive a project in their workspace. An admin of another workspace cannot change it.
- `AC-archive-2` — an archived project disappears from both active views.
- `AC-archive-3` — the archived record remains accessible through authorized history.

The baseline already has separate active and history entry points. The request extends the active-view filter and introduces an archive write. The history path keeps its existing retention behavior. The brief links the task and decision, names the current code revision, and scopes the change to those paths.

## 2. Trace the code and plan the checks

- **Write** — archive action → project service → workspace-scoped update of `archivedAt` → response.
- **Active readers** — list query and board query each read project state. Both must apply the same active criterion.
- **History readers** — history screen and export query read historical records with workspace scope.

The plan checks the write for authorized and foreign-workspace callers, checks the list and board after the write, and confirms that history still reads the same row. The feature PR records these checks against the reviewed head.

## 3. Review the first patch

The first patch adds the archive write and filters the list query. The board query still reads every project in the workspace. The direct read matters because archiving introduces a state the board previously did not need to filter.

**Important fix — before merge.** After a project is archived, the board still displays it because `board.js` queries workspace projects without applying the active filter. Reuse the active-project query for the board and verify both active views immediately after archiving. This closes `AC-archive-2` while history can keep its separate read.

Evidence at the first head: authorized archive and history retention pass, foreign-workspace mutation is denied, the list omits the project, and the board check fails. The reviewer reads both query paths and checks whether a caller already filters the board result. The retained finding describes the failing path and holds readiness for `AC-archive-2`.

## 4. Recheck the fix and the updated requirement

The revised patch uses the same active-project query for the list and board. A task update clarifies that historical export is part of acceptance, consistent with `D-08`. Record the new criterion as `AC-archive-4` and recheck the export path at the revised head. Preserve the first review's source reference so its original coverage remains clear.

The revised evidence shows that both active views exclude the row, history and export include it, and a foreign-workspace caller still cannot archive it. The record closes the board finding and states that this focused verification exercises the service and query paths with in-memory data. It leaves browser behavior and database integration for their own checks.

## 5. Refresh context after merge

- **Flow map** — add the archive write and the shared active query as evidence of current behavior.
- **Regression record** — link `AC-archive-1` through `AC-archive-4` to the code and checks.
- **Delivery** — link the PR and close the pending context refresh after verifying the landed commit.

The next agent receives the scope, accepted task revision, landed code revision, affected readers and writers, and the results above. It can reopen the relevant paths when a later change touches project lifecycle.
