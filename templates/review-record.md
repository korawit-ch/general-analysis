# Review record

Use with [Change review](../change-review.md). Keep the report with the PR or review task where practical.

## Target

- **Scope** — [Question, repository, changed areas, and coverage limits]
- **Revisions** — [Target branch and SHA, merge base, head SHA, or exact local diff]
- **Intent** — [Requirement and decision links, versions checked, approved deferrals]
- **Evidence available** — [Code, tests, CI, reproduction, reviewer and review date]

## Findings

Repeat for each actionable finding. Order by impact.

- **Finding** — [ID, priority and fix timing, pinned file and line]
- **Trigger and effect** — [Reachable scenario, expected behavior, who or what is affected]
- **Evidence** — [Code trace or reproduction and any counterevidence checked]
- **Correction and disposition** — [Smallest useful fix, verification, open or rechecked at new head]

## Coverage

- **Each changed file** — [Path and lines, action, responsibility, behavior, and fit with the project]
- **Each criterion** — [Criterion and source → implementing path → actual check and revision → result or gap]
- **Each material external effect** — [Affected path or consumer, what was checked and remaining gap]

## Readiness and handoff

- **Checks** — [Command or CI link, revision, scenario, actual result and limit]
- **Verdict** — [Ready, conditional, or blocked, with evidence and outstanding decisions]
- **Re-review** — [What changed since prior review, checks repeated and findings closed]
- **Rollout and context** — [Required order, action, owner, verifying signal, affected context and refresh owner]
