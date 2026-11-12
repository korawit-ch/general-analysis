# Analyze an ongoing project

Establish what the analysis must help someone do. Onboarding needs a map of the system and where to start. Planning a feature needs the existing path, ownership, and adjacent consumers. An architecture assessment needs the boundaries, risks, decisions, and evidence that would justify a change.

## 1. Identify the system and sources

- Confirm the repository or repositories, intended branch or revision, task or question, and areas in scope. Run `git status --short --branch` before working in a checkout. Record existing changes and inspect committed sources separately when they differ.
- Read the root and relevant nested instructions, README, workspaces or build definitions, test config, and CI. Follow the real entry points and module registrations. In a multi-repo system, pin each relevant repository independently and identify shared data or contracts.
- Locate the project’s owning requirements, accepted decisions, design, and runbooks. Record only the relevant sections and their version or last-read time. Keep the observed code revision independent of the version of the requirement.
- Verify that the available checkout represents the question being asked. A feature branch can show work in progress. A merged source revision can show what landed. Deployment requires its own evidence.

Use a [source register](templates/project-context.md#source-register) when several inputs need to be reconciled. Treat dated or incomplete docs as leads. Record a concrete question, its consequence, and an owner when the source needed to settle it is missing.

## 2. Map the project top down

1. **Purpose and actors.** Name who uses the system, what they need to do, and which actor owns each critical operation. Include background jobs, external callers, and operators where relevant.
2. **Runtime and deployment.** Map entry points, deployable units, stores, caches, jobs, and external systems. Follow startup and deploy definitions to distinguish runtime modules from shared libraries, tooling, generated code, and examples.
3. **Module ownership.** For each important area, record its responsibility, entry files or symbols, callers, dependencies, public interfaces, and state changes. Identify the owners of features, permissions, contracts, reusable UI, configuration, and database writes. Use [Code and data](guides/code-and-data.md) for the placement and boundary questions.
4. **Data model.** Record important entities and relationships, authoritative writers, lifecycle states, tenancy, retention, and integrity constraints. Check the schema and migrations where they matter. Inspect the actual write path to see how a rule is enforced.
5. **User journeys and critical flows.** Choose three to six when mapping a whole project, or just the affected flows for a targeted task. Explain the actor’s goal, actual path, negative cases, and outcomes visible to the user or downstream systems. Use a [Flow record](templates/flow-record.md) for a flow worth retaining.
6. **Checks and operations.** Locate commands and prerequisites in the project’s scripts, config, and CI. For each relevant check, state what it proves, which environments it uses, and where its coverage ends. Link actual run evidence when available.

A map should let a new contributor answer “where do I change this?” Include a few common changes and link the owner, entry point, and closest relevant check. Group modules by stable responsibility. Branch status, release dates, and task counts can stay with the systems that own them.

## 3. Separate facts from judgments

- **Observed in source** means the inspected revision supports the claim. Cite the file, symbol, or pinned line.
- **Verified by execution** means a named scenario ran at a known revision and produced a recorded result. State the environment and data setup where they matter.
- **Accepted requirement or decision** means an owning source or authorized decision maker agreed to it. Link that source.
- **Inferred** means evidence supports a reading without settling it. Record what would confirm or disprove it.
- **Proposed** means a change, standard, or target awaits a decision. Name the owner and the consequences of adoption.

If a document contradicts code, preserve the distinction between current behavior and intended behavior. For example, a spec may say that exports include every project, while the current implementation excludes archived rows. Record the discrepancy and find whether a decision, regression, or unfinished feature explains it.

## 4. Record risks and close the analysis

Retain risks with a concrete trigger, affected actor or consumer, consequence, evidence, owner, and next check or decision. Distinguish an existing defect, a gap in the accepted specification, a proposed improvement, and an investigation gap. Prioritize the issues that could change the next plan or review.

Use [Project context](templates/project-context.md) as the compact output. Link existing records for deeper capability specs, delivery plans, or runbooks. Write the overview after verifying the underlying claims. For an ongoing project, refresh the affected parts using [Context maintenance](guides/context-maintenance.md).
