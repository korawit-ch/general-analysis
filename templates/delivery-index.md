# Delivery index

Generate this from the hosting service and Git. Do not copy tracker statuses or descriptions into it; they go stale. Replace the bracketed prompts.

## Source and regeneration

- **Repository and revision** — [Repository, default branch commit, date read]
- **Commands** — [The exact listing and ancestor-check commands used, so the index can be rebuilt]
- **Rule** — A merged change request is on the default branch only when its merge commit is an ancestor of it, or when the same patch is present under another commit.

## Change requests

Repeat per change request.

- **Number and title** — [Number, short title]
- **Tracker items named** — [Keys, or none]
- **Base** — [Default branch, or stacked on which branch]
- **State and merge date** — [Open, merged with date, or closed]
- **On the default branch** — [Yes, no, yes by patch content, or unclear with the reason]

## Merged but not on the default branch

- [Change request] — [Evidence, and which open work would bring it in]

## Tracker item to change requests

- [Key] — [Epic or parent] — [First sprint or milestone] — [Change requests]

## Change requests with no tracker item

- [Change request] — [What rule or behavior it changed]

## Not verified

- [For example: remote not fetched, bodies and diffs not read, later reverts not checked]
