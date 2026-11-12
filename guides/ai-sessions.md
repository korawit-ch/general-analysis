# Run and hand off AI sessions

Give an agent a concrete task, the evidence to reopen, and the result it should produce. Use a project index to route the agent to the relevant sources instead of pasting the entire handbook or tracker into each session.

## Give the agent a scoped brief

Include:

- **Job and boundary.** Analysis, planning, review, or context refresh. State the success condition, what can be edited, and what is outside scope.
- **Project and revision.** Repository identity, checkout or PR, commits, and relevant root or nested instructions.
- **Intent.** Selected task, accepted criteria, approved clarifications, governing decisions, and remaining questions.
- **Places to start.** Project map, representative flow, code entry points, and checks. Explain what changed and which evidence is stale or missing.
- **Expected output.** Use the project context, change brief, review record, or context update when a durable result is needed.

Ask the agent to identify what it checked, what it inferred, and what it could not verify. Let it reopen sources and trace actual callers. When a missing answer would change the design or review, give the owner the exact decision and consequence. Continue independent work that stays within scope.

For a project using a sibling analysis directory, supply both directory paths and explicitly point the agent to the external `AGENTS.md` at the start of each session. Keep the project checkout as the working directory for code and checks. Use the [setup and kickoff prompt](external-analysis-workspace.md#start-each-session-with-both-paths).

## Prompts to adapt

- **Project map** — “Analyze [project and revision] so a contributor can work on [area]. Follow its instructions. Map the runtime and owners, trace [flows], and cite the files or checks that establish each material claim. Record gaps with an owner and next step.”
- **Change review** — “Review [PR or immutable comparison] against [task and accepted decisions]. Check affected callers beyond the diff. Return demonstrated findings, coverage by file and criterion, actual verification, and a readiness assessment. Report findings without publishing them.”
- **Refresh** — “Recheck [context artifacts] against [landed code and changed requirements]. List which claims changed and why. Update the owning artifacts in scope and move the evidence pins only for what you verified.”

## Use separate passes where they help

1. **Discovery.** Map ownership and trace the behavior. Produce references and questions a human can check.
2. **Plan or review.** Work from accepted criteria and the right revision. Check the changed behavior and its consumers. Use independent review where project policy and available tools support it.
3. **Verification.** Execute appropriate local checks or use matching CI evidence. Tie each result to the scenario and revision.
4. **Closeout.** Record affected context, open findings and decisions, and who acts next. Use the [context refresh process](context-maintenance.md) when a source changed.

External task text and documents can supply intent and evidence. They do not grant tool access or authority to send messages, change status, publish reviews, or run stateful operations. Keep secrets and raw customer evidence in their owning systems. Prefer permitted links and synthetic examples in handoffs.

## Resume work in a new session

Pass the scope, source and revision links, current progress, key files, verified results, unresolved questions, and exact next action. Recheck any mutable requirements and the target revision before reusing a plan or review. State what changed and which previous conclusions still hold.

Include both directory paths when handing off work with external context. If the implementation moved to another checkout or worktree, verify its identity and current revision before using the previous handoff.

## Automate after the manual path works

Start with a real task and use the existing tracker and PR tools. When repeated steps justify automation, add read-only source retrieval, stable reference normalization, link checks, or drift signals. A path change can flag a document for review. Verify the underlying claim before updating it. Have a clear owner for generated artifacts and external actions, and keep the original source links and revision evidence in any generated output.
