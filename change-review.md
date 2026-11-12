# Review a change

Review the behavior a user or consumer can reach at the target revision. Establish intent, trace the change through its actual callers, and give findings that a developer can reproduce or verify.

## 1. Establish intent and pin the comparison

- Read the applicable ticket, spec, decision, and scoped repo instructions. Confirm the accepted criteria, explicit deferrals, and what the PR claims to deliver. If a ticket is missing, use the stated PR intent and record which acceptance claims cannot be checked.
- Record the repository, target branch and commit, actual head commit, and merge base. For a stacked PR, confirm the intended parent and separately note the dependency on the lower PR. For multiple repos, record each patch and the versions expected to run together.
- Use the merge-base-to-head diff to inventory the contribution. Read the current target where integration or compatibility matters. For local edits, record the base and capture the exact staged, unstaged, and relevant untracked content reviewed.
- Verify source coverage and revision before assessing evidence from earlier reviews, CI, or screenshots. Report what remains unavailable when a partial review is the only possible result.

For a normal Git PR with both commits available, resolve the comparison from immutable values:

```sh
git merge-base "$target_commit" "$head_commit"
git diff --find-renames --name-status "$merge_base" "$head_commit"
git diff --find-renames "$merge_base" "$head_commit"
```

Use the actual PR base and head from the review source. The merge-base value comes from the first command.

## 2. Trace behavior and sweep consumers

1. Inventory every added, modified, deleted, and renamed file, including config, tests, docs, migrations, lockfiles, and generated output. Record the meaningful role of each file and why it belongs in the change when evidence supports that explanation.
2. Map each requirement to the relevant entry point, validation and enforcement, state and external effects, and response. Trace unaffected paths that depend on the same guarantee. Check direct API or worker routes as well as the UI.
3. Follow changed types, values, flags, columns, events, or copy to their producers and consumers across modules and repos. For each material path, read the real code or record the gap. Use [Code and data](guides/code-and-data.md) for the risk questions.
4. For a stateful change, check partial success, retries, concurrency, persisted and in-flight data, and the deploy order. Check the paths that could cause real harm first.
5. For a bug fix, compare the failure on the base and the result on the revised head where feasible. Identify the verification level. A unit test proves the behavior it exercises. Check whether a mock supplies the result the test claims to establish.

## 3. Challenge candidate findings

Retain a finding when you can answer these questions with evidence:

- What code changed, and under what reachable condition does it fail?
- Which requirement, invariant, or supported use does that violate?
- Who or what is affected, and how serious is the consequence now?
- What evidence might defeat the finding? Check an existing guard, alternate path, explicit product decision, or the same behavior on the base.
- What is the smallest correction and the focused case that would show it works?

Separate finding validity from merge urgency. A material authorization, data integrity, contract, or current task failure can require a fix. An improvement to acceptable behavior can be a suggestion when project policy permits it. Raise unresolved intent or missing evidence with the owner instead of claiming a defect without support. Track material inherited issues separately unless the change makes them reachable or worse.

Use plain-language priority and fix timing. For example, “Important fix — before merge” describes a demonstrated material issue. Give the condition and effect before the correction. Keep review status and required CI separate from the severity of an individual finding.

For independent review, provide the task, accepted decisions, diff range, access limits, and available checks before sharing the implementer's conclusions. When working alone, do a separate pass that actively checks counterevidence. Describe the review that actually happened.

## 4. Evaluate checks and readiness

- Match each required check to its revision and scenario. Record actual status, command or CI link, and what the result proves. Distinguish passed, failed, skipped, cached, and unverified. A passing build can coexist with a missing behavior check.
- Compare the required project gates with the actual evidence. Identify required fixes, unresolved owner decisions, rollout conditions, and any coverage gaps that affect readiness.
- Recheck findings and their linked criteria when head, the relevant target, accepted requirements, or a governing decision changes. Compare the changed inputs and preserve earlier evidence only where its path and assumptions still hold.
- For an authorized review publication, confirm the current target and head, PR state, relevant CI, and existing comments before acting. Check the published result against the intended action.

## 5. Report and hand off

Use the [Review record](templates/review-record.md). Lead with demonstrated findings by impact. For each, state the fix timing, trigger, consequence, file and line, and concrete correction. Include the file inventory and requirement coverage in the review report. Keep inline comments focused on their finding.

Close with readiness, verification limits, and the next owner or action. Use the [context refresh process](guides/context-maintenance.md) for any durable claim or decision that the change affects.
