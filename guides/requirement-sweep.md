# Sweep requirements across every source

Use a sweep when an analysis has drifted from the project, when several sources describe the same product differently, or before a phase whose tickets are thin. A sweep compares the prototype, the code on the default branch, the change requests, the tracker, and the product documents, then turns the differences into findings, corrections, and questions.

## 1. Pin every source before reading

- Record the default branch commit, the prototype commit, and the read date of the tracker and each document. Read code from an export or a detached copy of the pinned commit when the working checkout is on another branch or has local changes.
- Find the prototype's source, not only its deployed site. The source shows which logic is mock; the site shows only the result.
- List what will not be read, and why. Pages that hold credentials or personal data are named and left closed.

## 2. Split the work so results can be trusted

- **Divide by module for reading.** Give each pass one module and the same output sections: prototype inventory, current state, change request and ticket check, conflicts, code suggestions, documentation gaps, items with no ticket, product questions, and what was not verified.
- **Divide by target file for writing.** When passes edit records, give each pass its own set of files. Several findings usually correct the same record, so dividing by finding puts two writers on one file.
- **Give every pass the same rules.** Read only, no deployed environments, no credentials, cite a path and line at the pinned revision, and report what was not verified.
- **Label how far each claim was checked.** Confirmed means a second reader re-read the cited lines. Reported means one pass stated it. Inferred means it follows from the code and needs a run to prove. Keep these apart in the summary.

## Classify prototype logic

A prototype is usually authoritative for layout and wording, and unreliable for logic. A ticket that says "follow the prototype" hides that difference. Classify each screen element:

- **UI to copy.** Layout, labels, states, and interaction that the design owner intends.
- **Rule candidate.** Behavior that looks like a business rule. It becomes a requirement only when a ticket, product document, or decision confirms it.
- **Placeholder.** Logic written to make the screen work: mock data, hard-coded values, arithmetic chosen for display, stand-in toggles, demo tools. Never copy it.

Signs of a placeholder: totals that disagree between two places on the same screen, a rule that fires in a case where it makes no sense, a value derived for display and never stored, validation that accepts an impossible value, a warning whose promised effect never happens, and anything read from a mock file or constant.

Re-read each placeholder in the prototype source before recording it, and record the result in a [prototype classification](../templates/prototype-classification.md). Check the product code for placeholders it has already copied.

## 3. Check what actually landed

- **Merged does not mean on the default branch.** A change request stacked on a feature branch reaches the default branch only when its root merges. Test each merge commit with `git merge-base --is-ancestor <commit> <default branch>`. When that fails, compare patch content with `git patch-id` before concluding, because a rebase gives the same change a new commit.
- **Tracker status does not describe the branch.** Build a [delivery index](../templates/delivery-index.md) from the hosting service and Git, and use it to answer "is this on the default branch".
- **Find rule changes with no ticket.** List change requests that name no tracker item and read what each one changed. A rule that shipped this way is a decision nobody recorded.
- **Read done tickets against their criteria.** A closed ticket with an unmet criterion is a finding.

## 4. Turn differences into the right kind of record

- **A defect in code** goes to the code owner with the trigger, consequence, path and line, and the smallest correction.
- **A conflict between sources** goes to the conflict list with both sides quoted. Do not choose a winner.
- **A settled question** goes to the decision log only when a dated source shows someone with authority decided. An engineer's note on a ticket is evidence of intent, not a product decision.
- **An unanswered question** goes to the single open-questions list with the tickets it blocks.
- **A stale statement in the analysis** becomes a correction with the corrected fact and its citation.
- **A missing document** is recorded against its [package topic](analysis-package.md).

## 5. Apply corrections safely

1. Save a copy of the records before editing when they are not under version control, so the change can be shown as a diff. Put the analysis under version control as soon as it has more than one editor or one refresh.
2. Before applying a correction about code, open the cited lines at the pinned revision. Apply what the source shows. Sweep reports carry small errors in line numbers and scope, and this step catches them.
3. Write the current behavior only. History belongs to version control or a dated update record.
4. Keep dated reports and update records as written. Record later corrections in a new dated record.
5. Ask each editing pass to list the stale lines it saw that were outside its list, and to say per file whether every code statement was re-read. Move a freshness state only as far as that answer supports. See [Context maintenance](context-maintenance.md#decide-what-to-recheck).
6. Treat a drifted line number as a reason to read the code. Re-reading stale citations regularly surfaces real defects.

## 6. Report

Lead with the findings to act on first: security and data scope, then broken flows, then money. Follow with the patterns behind them, the prototype placeholders, the conflicts that block upcoming work, the document gaps by package topic, and what was not verified. State plainly that nothing was executed when that is the case.
