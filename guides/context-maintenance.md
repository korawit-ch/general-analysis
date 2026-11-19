# Maintain context as the project changes

Project analysis is a set of claims about sources that move independently. Record what each artifact owns, which evidence backs it, and which change would make it unreliable.

## Give each artifact an owner

- **Intake and source register.** Keep links to scoped source material, its version or date, and unresolved conflicts. Leave sensitive evidence in its owning system.
- **Project map and flows.** Explain the current system, its runtime and code ownership, and relevant invariants at an inspected revision.
- **Package index.** List the twelve [package topics](analysis-package.md) with the state and owning record of each. Update a topic's state when its record changes.
- **Requirements and decisions.** Keep accepted criteria, proposals, and decision records with their owners. Record why a material decision was made, which areas it affects, and any decision it supersedes. Use the project's established history format. Keep one [decision log and one open-questions list](../templates/decisions-and-questions.md); other records link to a row and keep no copy.
- **Delivery index.** Generate the map of change requests, tracker items, and what reached the default branch from the hosting service and Git. Regenerate it; do not hand-edit it or copy tracker statuses into it. See the [template](../templates/delivery-index.md).
- **Prototype classification.** Pin it to the prototype's commit and update the touched rows when the prototype changes.
- **Delivery and forecasts.** Track deliverables, dependencies, and gates in the owning plan. Keep estimate inputs or forecasts at their source. A forecast describes what may happen under stated assumptions. The plan records intended sequencing and readiness criteria.
- **Implementation and review.** Keep the task plan and PR evidence linked to the project map and requirements. Separate reports or snapshots can record their coverage and verification revisions.

Group durable analysis by stable capability or owning boundary. Keep transient tracker statuses and counts at their source. If the project already owns a fact in a handbook, tracker, ADR, or runbook, link it and update it there when needed.

Start with an index and project map in the chosen home for analysis. Use an [external analysis workspace](external-analysis-workspace.md) when assistant instructions and context belong outside the project. Give complex flows a small record per capability as they become useful. Link accepted requirements, plans, and decisions from their owning records. Give each analysis area a project revision and owner so readers can identify the code it describes.

## Decide what to recheck

- **Merged code or config.** Entry points, public exports, schema, auth, shared state, or runtime changes can invalidate the map, flow, rollout note, and regression criteria.
- **Requirement or accepted decision.** Trace it through affected criteria, design assumptions, delivery gates, implementation, and reviews. Resolve disagreements with the owning decision maker.
- **PR base or head.** Recheck the paths, consumers, criteria, and checks affected by the comparison change. Treat claims about rollout or integration separately from patch behavior.
- **Evidence or access.** If a source disappears, is revised in place, or becomes inaccessible, keep the previous verified point and record what needs rechecking before use.

Track freshness per area when the whole project cannot be verified together. `Current` means every claim in the record was checked against the named revision or source. `Corrected` means the listed claims were checked and fixed while other lines keep an older pin; name those lines where the reader will find them. `Pending` means a known change may affect it. `Unverified` means the evidence is missing or insufficient. Keep the last verified point and the candidate target visible when they differ.

## Apply an update

1. Name the trigger and pin the old and new sources. For Git history, compare from the previous verified commit when it is an ancestor of the target. If history diverged, find the common ancestor and inspect both sides for claims that may have changed.
2. Make an affected-artifact list. Record each changed claim, owning file or record, and how it will be verified. Follow links from changed requirements and boundaries through downstream docs and tests. Use changed paths as leads and confirm impact by following behavior.
3. Update the owning artifact and its dependent references. In the same repository, include affected durable docs with the implementing change where practical. In a separate analysis workspace, link the implementing PR and leave affected claims pending until verified against the landed revision.
4. Confirm each correction about code in the source before writing it, including corrections that come from a report. Ask whoever edits a record to say whether every code statement in it was re-read, and to list stale lines outside their task. Use `Corrected` until the answer is yes.
5. Read the result against the new evidence. Verify links, assumptions, and any retained evidence. Move the pins only for areas actually rechecked. Record the remaining owner, decision, or check.

Use a [Context update](../templates/context-update.md) for material changes. Keep accepted decision history and revision links when a future agent will need to understand an earlier review or scope choice.
