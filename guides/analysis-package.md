# Structure the analysis as a package

Use this guide when the analysis must stand as a complete requirement package for a product or a large feature, and when checking whether an existing analysis has gaps. The package runs top down, from who the user is to how the work is delivered. Evidence gathering often runs bottom up, from code, tickets, and prototypes. Keep both: the package says what should be true and how it will be built, and the evidence layer says what is true now and where the two disagree.

## The twelve topics

Work in this order. Each topic depends on the ones above it, so a gap near the top weakens everything below.

**Design: who it is for and how it behaves**

1. **Persona.** Each actor with their goal, working context, device, frequency of use, and what goes wrong for them today. A role name and a permission list are the start of a persona, not the whole of it. Include the people the system affects without an account, such as an end customer.
2. **Journey.** The end-to-end path of one persona toward one goal, across screens, people, and time, including waiting, handoffs between actors, and the unhappy endings. A journey crosses several process flows.
3. **User story.** Actor, need, and reason, each with acceptance criteria that state preconditions, action, and observable outcome. Link each story to its journey step and to its tracker item. An index of tickets is not a set of stories.
4. **Process flow.** The steps and decisions of one process by actor, with every state transition listed as actor, precondition, effect, and what happens on failure. Keep the business process apart from the code trace that implements it; link the two.
5. **UX/UI.** Screens, states (empty, loading, error, denied), field rules, responsive and language rules, and the design system. When a prototype is the reference, classify its logic before anyone copies it. See [Requirement sweep](requirement-sweep.md#classify-prototype-logic).

**Analysis: what to build and how**

6. **Specification.** Rules with stable IDs, the data dictionary, money and time rules with worked examples, contracts, and error behavior. Each rule names its source and its status: accepted, proposed, or in conflict.
7. **Architecture.** Runtime and deployment, module ownership, the data model, integrations, and environments. Use [Project analysis](../project-analysis.md) and [Code and data](code-and-data.md).
8. **Non-functional requirements.** Security, privacy and legal, performance, availability, backup and recovery, audit and retention, accessibility, localization, supported browsers and devices, and observability. Each needs a threshold, a way to measure it, and an owner who accepted it. See [Requirements and planning](requirements-and-planning.md#3-write-evidence-ready-acceptance).
9. **Development tasks.** The breakdown of each story into tasks with the code path, the checks, and a definition of ready. Use a [Change brief](../templates/change-brief.md) for a task that touches money, state, access, or files.
10. **Development plan.** Sequence, dependencies, decision gates, and rollout order. A record of past sprints is history; the plan looks forward.
11. **Resource, timeline, and budget.** People and roles, effort with the basis of each estimate, dates, and cost. These come from the people who own them. Link the owning plan and record the date read; do not derive them from code.
12. **Risk and mitigation.** Product, delivery, technical, and operational risks, each with a trigger, consequence, owner, and mitigation. Code-level risks are one part. Unanswered questions that block work are delivery risks and belong here too.

## Keep an evidence layer under the package

The topics have no slot for the records that keep them true. Maintain these beside the package and link them from every topic that relies on them:

- **Source register and freshness.** What was read, at which revision or date, and which areas are current. See [Context maintenance](context-maintenance.md).
- **Conflicts between sources.** Where the prototype, tracker, product documents, and code disagree. A conflict stays a conflict until an owner decides.
- **Decision log and open questions.** One list of each. See the [template](../templates/decisions-and-questions.md).
- **Delivery index.** Which change request carries which tracker item, and whether it reached the default branch. See the [template](../templates/delivery-index.md).
- **Prototype classification.** See the [template](../templates/prototype-classification.md).

## Check coverage before starting work

Create the [package index](../templates/analysis-package.md) first, even when most topics are empty. For each topic record one state:

- **Covered.** The record answers the topic's question for the current scope and names its sources.
- **Partial.** A record exists but answers a narrower question. State what is missing.
- **Missing.** Nothing answers it. Name who can supply it.
- **Not applicable.** State why, so the next reader does not reopen it.

Then act on the result:

- A missing or partial topic above the one you are working on is a finding. Report it before building on it. For example, tasks written while the process flow lacks its state transitions will encode guesses about who may act and when.
- Fill a topic only from sources that can establish it. Personas, journeys, non-functional thresholds, and budgets need a product or business owner. Draft them from evidence if that helps, label every unconfirmed line as inferred or unknown, and name the owner who must confirm.
- Do not reorganize an existing analysis to match the package in one step. Add the index, let it prove useful, then move records when links can be updated together.

## Keep the package alive

- **A new requirement arrives.** Walk the topics top down and update each one it touches, starting with the persona and journey it changes. Stop at the first topic where a decision is missing and raise it.
- **A decision is made.** Add it to the decision log, update the rule in the specification, close the question, and recheck the stories and tasks that cited it.
- **A change lands.** Refresh the delivery index and the freshness of the areas it touched. See [Context maintenance](context-maintenance.md).
- **A review or sweep finds a gap.** Record it against the topic it belongs to, so gaps accumulate in one place.

Decide the audience once and state it in the index. A package for a client or a team reads as deliverables. A package for AI sessions is denser and cites sources line by line. The facts are the same; the form differs.
