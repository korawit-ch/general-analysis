# Analyze code, data, and runtime boundaries

Use this guide after locating the target area in [Project analysis](../project-analysis.md). Follow the project's real names and ownership model. Identify the established pattern and any explicit instruction that designates an older pattern as legacy.

## Understand where code belongs

- **Feature behavior.** Find the narrowest runtime and module that own the behavior. Inspect its public entry points and actual callers. If two modules have similar code, compare why they change before proposing a shared helper.
- **Reusable components.** Separate a UI primitive from a product-specific workflow. Identify who supplies state, copy, routing, validation, and permissions. Inspect design tokens, locale ownership, accessibility, and existing component APIs before adding a variant.
- **Constants and policy.** Find the owner of each shared value. A wire enum belongs to its contract, runtime defaults to validated config, style tokens to the design system, and business rules to the authoritative domain or service. Similar literals can represent independent rules. Centralize by meaning and change ownership.
- **Package boundaries.** Read public exports, dependency declarations, supported runtimes, build order, and actual imports. Identify what consumers depend on and who can change it. A package can be shared across apps when the interface has real consumers and a stable owner.
- **Validation and data mapping.** Identify which layer validates inputs, enforces business rules, and maps persistence objects to a public contract. Trace both runtime checks and compile-time types. Inspect error and null semantics along the path.
- **Generated code and tooling.** Find the source and generator for schemas, API clients, or assets. Record which files are edited and which are regenerated, and how CI detects drift.

Keep observed conventions in the project map. If ownership is split, document what each path does and the consequence of that split. Put a proposed consolidation in a decision or task with the intended owner and affected callers.

## Trace the running path

1. Start with a user action, HTTP request, command, scheduled event, or message. Find registration and dispatch so you can establish reachability.
2. Follow the actual validation, authentication, and authorization. Find where resource scope is derived and enforced, including in the final read or write.
3. Follow domain logic through persistence, caches, queues, storage, and external calls. Record transaction or commit boundaries, message identity, retries, and side effects in order.
4. Follow the response and all consequential effects back to the user or consumer. Check invalidation, polling, notifications, logs, and visibility in related surfaces.
5. Look for other callers of the same behavior and other producers or readers of the same state. Search by meaning as well as symbol, using alternate routes, shared schemas, message names, migrations, tests, and documented contracts.

Capture a meaningful normal path and the negative cases that could change a review decision in the [Flow record](../templates/flow-record.md). State what was directly checked and what remains an inference.

## Check the boundaries that matter

- **Authority.** Can a caller bypass the UI and invoke the same effect through another route, job, or integration? Does the server enforce the rule using trusted identity and current state?
- **Consistency.** Where is the first durable write? What is visible after an error between a write and a second effect? Can a retry or concurrent request duplicate a transition or overwrite a newer value?
- **Versions.** What happens to old rows, messages, drafts, cached responses, and open tabs? Can old and new producers and consumers coexist? Record the required order and evidence for migration or rollout.
- **External systems.** Check error classification, timeouts, retry limits, idempotency, and whether a successful local response means the external change was confirmed.
- **Operations.** Identify how a real failure is detected and recovered. When optional work fails, check whether essential behavior still works. Inspect hot-path queries, log volume, and exposure of sensitive values where relevant.
- **Visible behavior.** Follow changed names, availability, and state through other screens, empty and error states, locale files, accessibility labels, docs, exports, and notifications that use them.

For an impact sweep, start with the changed concept and follow its readers, writers, and callers across boundaries until the reachable affected paths are accounted for. Record unresolved paths and their consequence. Report unrelated defects separately from the change under review.
