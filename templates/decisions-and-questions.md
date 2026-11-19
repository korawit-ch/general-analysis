# Decision log and open questions

Keep these as two records with one list each. Other records link to a row here and do not keep their own copy. Replace the bracketed prompts.

## Decision log

Newest first. Log a decision only when a dated source shows that someone with authority made it. A note by an implementer, a request from a client, and a rule that shipped without a ticket are not decisions; keep them as open questions and cite them as evidence.

- **ID and date** — [Stable ID such as DEC-001, date decided]
- **Decision** — [One sentence]
- **Source** — [Owning ticket, document section, or meeting record, and who decided]
- **Replaces or conflicts with** — [Earlier decision, rule, or source]
- **Reflected in code** — [Yes, no, or partly, with path and revision]
- **Reflected in tracker and documents** — [Yes or no, with links]

### Rule changes that shipped without a ticket

- [Change request] — [Rule it changed] — [Unconfirmed until an owner accepts it]

## Open questions

Put the questions that block current work first, then group by module.

- **ID** — [Stable ID such as Q-AREA-01]
- **Question** — [One sentence that an owner can answer]
- **What the sources say** — [Prototype, tracker, documents, and code, each with its citation]
- **Blocks** — [Tracker items that cannot proceed, or none]
- **Owner** — [Who can decide, or unknown]
- **From** — [Report, review, or record that raised it]

## Closing a question

1. Add the decision to the log with its source.
2. Update the rule in the specification and any story or task that cited the question.
3. Remove the question row, or point it to the decision if other records still link to it.
