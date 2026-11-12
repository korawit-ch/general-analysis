# Flow record

Record one real action or trigger. Keep paths and symbols specific enough for another person to reopen the trace.

## Entry and scope

- **Actor or trigger** — [User, external caller, job, or event and its preconditions]
- **Intent and outcome** — [What should happen and which requirement or invariant says so]
- **Revision and evidence** — [Repositories, commits, exact paths, and any check results]

## Path and effects

Repeat for the relevant steps.

- **Step** — [Path and symbol → who calls it → inputs and output → authority or state change]
- **Enforcement** — [Validation, authentication, permission and resource scope, final predicate or equivalent]
- **State** — [Data written, commit boundary, cache or queue, external effects and ordering]
- **Response** — [What the caller receives, what other consumers can observe]
- **Other paths** — [Alternate entry points, readers and writers, affected consumers and contract versions]

## Failure and verification

- **Failure or edge case** — [Trigger, visible result, persisted state, retry or recovery]
- **Concurrent and mixed versions** — [Race, old data or messages, deployment dependency where relevant]
- **Checks** — [Source inspection or executed scenario, result, and limits]
- **Refresh trigger** — [Changed rule, contract, path, or owner that could invalidate this trace]
