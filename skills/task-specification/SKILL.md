---
name: task-specification
description: Specify one task from an approved implementation plan as an evidence-based, implementation-ready coding-agent contract. Use for task specification and quality review; overall decomposition and dependency planning belong to implementation-planning. Framework-agnostic.
---

# Dev Task Specification

## Purpose
Turn **one approved plan entry** into a detailed coding-agent TASK specification with a cohesive, verifiable outcome. The planning skill owns milestone decomposition, ordering, and dependencies. **This skill specifies work; it does not implement it or silently replan.**

**Core rule: Delegate implementation, not engineering ownership. The model proposes; the application and human engineer decide.**

Read [task-standard](references/task-standard.md), [quality-gates](references/quality-gates.md), and [task-template](templates/dev-task.md). Consult the existing project's conventions and authoritative specifications. Follow applicable project-local workflow instructions (including AGENTS.md when present); do not assume files from another repository exist.

## Workflow

1. **Establish approved plan entry and source of truth.** Read the task ID, deliverable, dependencies, scope boundary, contract references, risk focus, and verification boundary from the approved plan. Record existing decisions, constraints, and unknowns; do not independently replan the milestone. Distinguish confirmed facts, evidence-based inferences, and proposals.
2. **Explore only enough to specify accurately.** For brownfield work, inspect relevant repository code, tests, migrations, architecture, docs, and callers *read-only* where needed to validate contracts and acceptance criteria. Do not repeat planning's broad decomposition or preempt the coding agent's detailed implementation Explore. For greenfield work, verify repository state, project structure, decisions, and prerequisite tooling instead of assuming a scaffold exists. If repository access is unavailable, mark findings unverified and prepare a bounded exploration task.
3. **Challenge the architecture before freezing the specification.** Identify the simplest approach consistent with approved contracts and existing mechanisms. Actively question assumptions when repository evidence suggests a materially better alternative. Compare meaningful alternatives by correctness, complexity, integration cost, and operational risk; do not manufacture three options when one is sufficient. Distinguish binding approved contracts from proposed implementation choices. Avoid speculative extensibility and defensive complexity without a concrete requirement or failure scenario. Record rejected alternatives only when doing so prevents repeated debate.
4. **Find gaps and conflicts.** Check domain semantics, data lifecycle, API contracts, security, trust boundaries, transactions, concurrency, failure behavior, side effects, observability, deployment, and testability *where relevant*. Do not mechanically require irrelevant fields. Present consequential decisions to the human with options and trade-offs. **Do not silently decide policy.**
5. **Validate the approved task boundary.** Confirm that the deliverable is cohesive, independently verifiable, and consistent with its plan dependencies. If evidence shows an incorrect boundary, missing prerequisite, or material scope conflict, propose a focused plan amendment for human approval; do not silently split, merge, renumber, or rewrite other tasks.
6. **Write the selected task specification.** Use the template without duplicating the same contract across sections. Include a short, evidence-based Implementation Explore Focus identifying likely components, assumptions to validate, and unresolved implementation questions; it is guidance, not a restriction on necessary investigation. Specify prerequisites, in/out of scope, invariant(s), acceptance criteria, happy/edge/failure/adversarial scenarios as relevant, verification commands or evidence, and stop conditions. Use stable IDs and explicit dependency references.
7. **Quality gate.** Apply all gates in `references/quality-gates.md`. Block only when an unresolved decision prevents a safe, bounded implementation exploration. Record implementation-level unknowns explicitly for the execution agent's explore phase rather than treating every unknown as a specification blocker. If essential evidence is missing, mark **NEEDS EXPLORATION**.
8. **Human review and handoff.** Present the selected task specification and decisions needed for approval; do not regenerate task ordering. Mark **READY** when the outcome, binding contracts, scope, and prerequisites are sufficiently clear to begin the implementation agent's read-only explore; implementation choices may remain open. Implementation handoff must require the coding agent to propose a plan, obtain approval at the agreed checkpoint, implement within scope, verify, report evidence, and submit diff for human acceptance.

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
1. **Plan reference:** approved task ID, dependencies, scope boundary, and authoritative contract links (without copying the plan).
2. **Decision log:** confirmed decisions, open questions, rejected assumptions.
3. **Task specification:** one Markdown file for the selected task, using the template.
4. **Specification readiness:** whether this TASK is READY for coding-agent EXPLORE, BLOCKED, or NEEDS EXPLORATION and why; do not confuse it with planning readiness or execution status.

Do not automatically generate all future task files when the user is still resolving architecture. Prefer incremental specification and review.
