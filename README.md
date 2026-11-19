# General project analysis

Use this field guide to understand an existing project, turn requirements into a plan, review a pull request, or refresh analysis after the code or decisions change. It works with the project's current architecture and delivery process. Start from the question the next person or AI agent needs to answer.

## Choose the starting point

1. **Repository or system.** Start with [Project analysis](project-analysis.md). Map the actors, runtimes, ownership, and critical flows. Use [Code and data](guides/code-and-data.md) for deeper traces and [Project context](templates/project-context.md) for the result.
2. **Ticket, spec, or decision.** Use [Requirements and planning](guides/requirements-and-planning.md). Reconcile the request with existing behavior and accepted decisions, then capture the scope and evidence in a [Change brief](templates/change-brief.md).
3. **Pull request or local diff.** Use [Change review](change-review.md). Compare the correct revisions, map each criterion to code and checks, and report demonstrated defects in a [Review record](templates/review-record.md).
4. **Existing analysis.** Use [Context maintenance](guides/context-maintenance.md). Identify claims affected by a change, then recheck and update them using a [Context update](templates/context-update.md).
5. **A project without assistant setup.** Use [External analysis workspace](guides/external-analysis-workspace.md) to keep assistant instructions, project context, and handoffs in a sibling directory. Give the agent access to both directories when implementing.
6. **A complete requirement package, or a check for gaps in one.** Use [Analysis package](guides/analysis-package.md). It orders the work into twelve topics, from persona to risk, and keeps an evidence layer under them. Start with the [package index](templates/analysis-package.md) and record what is covered, partial, or missing before building on it.
7. **Sources that disagree, or an analysis that has drifted.** Use [Requirement sweep](guides/requirement-sweep.md) to compare the prototype, the default branch, change requests, the tracker, and product documents. It produces a [prototype classification](templates/prototype-classification.md), a [delivery index](templates/delivery-index.md), and a [decision log and open-questions list](templates/decisions-and-questions.md).
8. **A new AI session or handoff.** Use [AI sessions](guides/ai-sessions.md) to give an agent the right sources and an explicit job. Use the [worked example](examples/archive-project.md) to see a ticket, code trace, review finding, fix, and context refresh together.

## How much to produce

- **One narrow change.** Add the relevant source, path, and verification to the existing task or PR. A short result can be enough.
- **A new contributor or an unfamiliar system.** Create a small project index with a system and ownership map. Trace a handful of flows that explain the main behavior and risks. Link to deeper analysis only where it answers a recurring question.
- **A cross-system or high-risk change.** Add dedicated flow, contract, data, requirement, and rollout evidence for the affected areas. Record missing sources and open decisions. Tie each delivery gate to an owner and a check.

Read in dependency order when you need the whole picture. The [analysis package](guides/analysis-package.md) gives that order for requirements: persona, journey, user story, process flow, and UX/UI, then specification, architecture, non-functional requirements, tasks, plan, resources, and risk. Evidence establishes the current system. Requirements and decisions define what must change. Architecture and a delivery plan describe how the work fits. Reviews test those claims against a specific revision. Update the smallest set of owning records that changed.

## What a complete result contains

- A scope, target revision or source version, and the sources actually consulted.
- A trace from a real actor or trigger through the relevant code, state, and side effects.
- A clear separation between observed behavior, accepted intent, inferences, and proposals.
- Coverage and verification limits that tell a reader what they can rely on.
- A next action, owner, or unresolved decision when work remains.
- For a package, the coverage state of each topic, so a reader can see what the analysis does not answer.

Use the templates as copyable prompts. Adapt their depth to the job and prefer the target project's existing docs, tickets, and PRs as the homes for durable knowledge. A separate analysis workspace can link to those sources and record when its claims were checked.
