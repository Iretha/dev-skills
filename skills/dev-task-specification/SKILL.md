---
name: dev-task-specification
description: Turn software requirements into small, evidence-based, implementation-ready coding-agent tasks. Use for backlog decomposition, exploration tasks, implementation specifications, and specification quality reviews. Framework-agnostic.
---

# Dev Task Specification

## Purpose
Convert a business/engineering goal into a dependency-ordered set of **atomic coding-agent tasks**. Each task has one primary verifiable deliverable. **This skill specifies work; it does not implement it.**

**Core rule: Delegate implementation, not engineering ownership. The model proposes; the application and human engineer decide.**

Read [task-standard](references/task-standard.md), [quality-gates](references/quality-gates.md), and [task-template](templates/dev-task.md). Consult the existing project's conventions and authoritative specifications. Prefer the engineering workflow in `curriculum/guides/AGENT-ENGINEERING-WORKFLOW-TEMPLATE.md` when available.

## Workflow

1. **Establish objective and source of truth.** Record the business problem, desired outcome, existing decisions, constraints, and what is explicitly unknown. Distinguish confirmed facts, evidence-based inferences, and proposals.
2. **Explore first, proportionately.** For brownfield work, inspect relevant repository code, tests, migrations, architecture, docs, and callers *read-only*. Exploration is the default, including when the engineer believes the solution is known. Keep it proportional. For greenfield work, verify repository state, project structure, decisions, and prerequisite tooling instead of assuming a scaffold exists. If repository access is unavailable, mark findings unverified and prepare a bounded exploration task.
3. **Challenge the architecture before freezing the specification.** Identify the simplest approach consistent with approved contracts and existing mechanisms. Actively question assumptions when repository evidence suggests a materially better alternative. Compare meaningful alternatives by correctness, complexity, integration cost, and operational risk; do not manufacture three options when one is sufficient. Distinguish binding approved contracts from proposed implementation choices. Avoid speculative extensibility and defensive complexity without a concrete requirement or failure scenario. Record rejected alternatives only when doing so prevents repeated debate.
4. **Find gaps and conflicts.** Check domain semantics, data lifecycle, API contracts, security, trust boundaries, transactions, concurrency, failure behavior, side effects, observability, deployment, and testability *where relevant*. Do not mechanically require irrelevant fields. Present consequential decisions to the human with options and trade-offs. **Do not silently decide policy.**
5. **Decompose by deliverable.** Build a dependency graph. Break down tasks until each has one main observable outcome, limited blast radius, clear ownership, and a meaningful verification method. Separate investigation, design decision, implementation, verification, and correction tasks when their outcomes differ. Avoid artificial micro-tasks with no independently useful deliverable. Prefer a cohesive vertical task when splitting would force repeated reconstruction of the same context; split only for a meaningful independent outcome, dependency, risk boundary, or verification benefit. Do not turn routine exploration, testing, review, or correction phases into separate backlog tasks by default.
6. **Write one specification per task.** Use the template without duplicating the same contract across sections. Include a short, evidence-based Implementation Explore Focus identifying likely components, assumptions to validate, and unresolved implementation questions; it is guidance, not a restriction on necessary investigation. Specify specify prerequisites, in/out of scope, invariant(s), acceptance criteria, happy/edge/failure/adversarial scenarios as relevant, verification commands or evidence, and stop conditions. Use stable IDs and explicit dependency references.
7. **Quality gate.** Apply all gates in `references/quality-gates.md`. Block only when an unresolved decision prevents a safe, bounded implementation exploration. Record implementation-level unknowns explicitly for the execution agent's explore phase rather than treating every unknown as a specification blocker. If essential evidence is missing, mark **NEEDS EXPLORATION**.
8. **Human review and handoff.** Present proposed task ordering, decisions needed, and specs for approval. Mark **READY** when the outcome, binding contracts, scope, and prerequisites are sufficiently clear to begin the implementation agent's read-only explore; implementation choices may remain open. Implementation handoff must require the coding agent to propose a plan, obtain approval at the agreed checkpoint, implement within scope, verify, report evidence, and submit diff for human acceptance.

## Interaction policy
- Ask targeted questions only when a decision blocks a useful next step; otherwise proceed with explicit, labeled assumptions and drafts.
- Never fabricate repository facts, file paths, APIs, test results, or commands.
- Do not equate passing tests with human acceptance.
- Never broaden the task to opportunistic refactoring.
- Optimize specifications for implementation efficiency, not brevity: invest in contract clarity and relevant evidence to prevent expensive rework.
- Preserve an independent implementation explore: it validates current code, can propose a better approach, and escalates any change to approved contracts for human decision. Specification proposals are not immutable architecture.
- Do not add requirements merely because a defensive mechanism is technically possible or generally considered best practice; justify complexity against actual risks and MVP scope.
- Avoid giant setup tickets; for greenfield projects start with minimal buildable scaffold, then add runtime, persistence, migrations, tests as independently verifiable increments.
- When asked to update a repository, create or update files only with available authorized tools; report links and what changed.
- Use the user's preferred language for discussion; specifications may use English if the project convention favors it.

## Outputs
1. **Task map:** ordered tasks with ID, type, deliverable, dependencies, status.
2. **Decision log:** confirmed decisions, open questions, rejected assumptions.
3. **Task specs:** one Markdown file per task, using the template.
4. **Readiness report:** which tasks are READY, BLOCKED, or NEEDS EXPLORATION and why.

Do not automatically generate all future task files when the user is still resolving architecture. Prefer incremental specification and review.
