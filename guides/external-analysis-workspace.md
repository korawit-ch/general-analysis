# Use a sibling analysis directory for assistant context

When a project has no assistant setup, pair its checkout with a sibling analysis directory. The analysis directory supplies instructions, project context, and handoffs. The project checkout supplies the code, existing engineering rules, and verification commands. Include both when starting an implementation session.

## Set up the analysis directory once

```text
workspace/
  example-project/           project checkout
  example-project-analysis/
    AGENTS.md                instructions for working with the paired project
    PROJECT.md               project identity, sources, and context index
```

1. Use the [external AGENTS.md template](../templates/external-agents.md) for the analysis directory's `AGENTS.md`. Use the [Project context template](../templates/project-context.md) for `PROJECT.md`.
2. In `PROJECT.md`, name the target repository by its stable identity and record the usual checkout location relative to the analysis directory where practical, such as `../example-project`. The session supplies the actual checkout or worktree for the task. Keep the last verified project revision with the claims it supports. For a non-Git project, identify the source and snapshot or version you inspected.
3. Record the actual entry points, local commands, and evidence sources the next agent needs. Look for conventions in the project's contribution docs, build manifests, CI, tests, and established code. Write down verified practices and label unresolved choices.
4. Add separate flow, decision, or task records as they become useful. Link them from `PROJECT.md`. Keep routine instructions in `AGENTS.md`, facts and source links in `PROJECT.md` or its linked records, and current task state in the task or its handoff.

## Start each session with both paths

Start the session in the implementation checkout and include the analysis directory in the same workspace when the tool supports multiple directories. Otherwise, give the agent the absolute analysis path and ensure the session can access it. Name the external instructions explicitly so the workflow works with manual loading.

> **Project checkout** — [absolute path to the checkout or worktree for this task]
>
> **Analysis directory** — [absolute path to the paired analysis directory]
>
> **Task** — [request or task link, intended outcome, and scope]
>
> Read `AGENTS.md` and `PROJECT.md` from the analysis directory first. Verify that the project checkout matches the recorded repository and the task's intended branch or revision. Read applicable instructions and the relevant code in that checkout. Use the project checkout for implementation and checks. Keep assistant instructions, reusable context, and handoff records in the analysis directory.

Before editing, confirm both directories are readable and that the session can write where the task requires it. For a Git project, check the actual checkout with `git -C "<project path>" rev-parse --show-toplevel`, `git -C "<project path>" status --short --branch`, and `git -C "<project path>" rev-parse HEAD`. Confirm the repository identity against `PROJECT.md`. An approved worktree can have a different path and revision from the usual checkout. If the checkout is ambiguous, resolve the target before editing.

If the analysis directory is read-only, return the proposed context update and its intended path. If the agent cannot read it, continue independent investigation in the project and identify the missing context. Restore access or obtain the relevant instructions before editing any part that depends on them.

## Use and refresh the context

- **Before implementation.** Open only the records relevant to the task. Recheck their claims against current code and approved requirements. Follow applicable project rules when they exist. Use the analysis instructions to fill gaps, and surface any material conflict.
- **During implementation.** Edit the authorized project files and run the project's checks from the project checkout. Save assistant-only notes, plans, and evidence in the analysis directory when they add durable value. Use repository-relative paths with a repository identity and revision for code references so they survive a moved checkout.
- **At handoff.** Record the project path, task source, branch or commit, relevant code paths, actual checks, open questions, and next action. Keep branch-specific evidence with the task. For uncommitted work, record the base and the relevant local diff state. Link the existing task or PR when it already carries the details.
- **After a project change lands.** Recheck affected claims against the landed revision before advancing their verification records. Leave uncertain entries pending and keep the last verified revision. See [Context maintenance](context-maintenance.md).

A later session can reopen the same two paths, read `AGENTS.md` and `PROJECT.md`, and load the latest relevant handoff. Update the analysis only when a reusable fact, decision, or pending action changes.
