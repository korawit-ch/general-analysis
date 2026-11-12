# Reconcile requirements and plan the work

Use the current project map to find affected owners and flows. The owning task, specification, and accepted decisions establish what the project is trying to deliver. Code and executed checks show how much already exists.

## 1. Collect the inputs

- For Linear, Jira, or ClickUp, record the provider, workspace or project, stable item identity, display key, and URL. For a Notion page or database item, link the relevant page and section or block. For other sources, use their equivalent stable link.
- Record the source version or updated time if available, the time you read it, and the exact passage that establishes each material criterion. Keep a stable local criterion ID if external display keys can change.
- Read the links that govern acceptance, scope, or ordering. Capture an attributed clarification only after checking who can make that decision. Keep open questions, estimates, and discussion distinct from accepted requirements.
- Identify the target repo and revision. If an input is inaccessible, use an authorized excerpt when available and state which conclusions remain unverified.

## 2. Reconcile each material requirement

Match incoming criteria to existing requirements and code by capability and behavior. Record the source, owning feature and system, expected behavior, current evidence, status, and next action. The status should explain what happens next.

- **Covered.** Link the existing criterion and code or test that supports it. If verification is partial, name the missing path.
- **Extends an existing capability.** Record exactly what the new input adds, the current boundary it changes, and which existing guarantees still apply.
- **New.** Identify the owning module or a decision needed to establish ownership. Keep scope and dependencies explicit.
- **Owned elsewhere.** Name the responsible system or team. If it gates this change, capture the handoff and what will prove readiness.
- **Conflict or unresolved.** Quote or link the competing passages, explain the consequence, and identify who can decide. Continue only the work that is independent of that decision.

Keep criterion IDs stable so tasks, code reviews, and checks can cite them in both directions. When a criterion changes materially, preserve an accessible revision link or authorized change note if an earlier review depends on the old wording. Reuse the project's existing IDs where possible.

## 3. Write evidence-ready acceptance

For new or changed behavior, describe the actor and preconditions, action, and observable outcome. Add data integrity or authorization criteria when the work changes state or access. Add failure, retry, concurrency, accessibility, or other edge criteria when those paths can affect acceptance.

For shipped behavior, a compact set of regression invariants is usually enough. Link the current implementation and the tests that protect the invariants. Where the code and a stated requirement diverge, keep the gap visible.

For a non-functional requirement, record the failure it addresses, the affected scope, threshold and measurement method, check or telemetry, owner, and approval status. A proposed latency or retention value stays proposed until an authorized owner accepts it. Record missing instrumentation as a dependency when it prevents verification.

## 4. Plan at two levels

- **Delivery plan.** For larger work, divide it into deliverables that can be accepted independently. Record an owner, dependencies, acceptance evidence, rollout order, and decision or external gates. Keep duration, engineering effort, and the basis of estimates explicit. Link status and dates to the owning tracker or plan.
- **Task implementation plan.** At pickup, inspect the current code and write the steps at the depth needed for the risk. Name reusable paths, what will change, the checks for each criterion, and how compatibility or recovery will be verified where applicable.

Use the existing task or PR for a short plan. Use a versioned plan for multi-step coordination, significant design decisions, or rollout work that several people need to share. Keep one active plan and link it from the other surfaces. Update it when accepted scope changes.

## 5. Handoff to implementation and review

Use the [Change brief](../templates/change-brief.md). Each criterion needs a source, an intended code path, and a verification method. Record approved scope, exclusions, conflicts, and dependencies. Recheck mutable sources before implementation resumes or a review closes. Use [Change review](../change-review.md) to assess actual evidence at the reviewed revision.
