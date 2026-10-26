---
name: dev-implementation-planning
description: Create or optimize a dependency-ordered software implementation plan from approved requirements and architecture. Minimize unnecessary agent cycles and repeated context reconstruction without sacrificing code quality, testability, risk isolation, or human decision ownership. Supports CREATE and OPTIMIZE modes.
---

# Dev Implementation Planning

## Purpose

Plan **what implementation tasks are needed, how to bound them, and in what order**. Optimize the total cost of delivering *human-accepted, verified behavior*, not the raw task count, prompt length, or an invented token estimate.

**Human ownership:** The human decides business semantics, architecture, MVP scope, risk acceptance, and final plan approval. The model proposes task boundaries, ordering, and trade-offs. Do not silently change approved contracts.

**Boundary:** This skill produces or revises an implementation plan; it does not implement code, write detailed per-task specifications, approve decisions, or mark tasks DONE. The task-specification skill turns approved plan entries into detailed TASK files; it should not independently replan the whole backlog.

Read [planning-standard](references/planning-standard.md), [quality-gates](references/quality-gates.md), and [plan-template](templates/implementation-plan.md). Follow the repository's authoritative requirements, architecture, and conventions.

## Modes

- **CREATE:** Draft a new implementation plan from approved requirements, architecture, and verified project state.
- **OPTIMIZE:** Assess an existing plan for unnecessary fragmentation, repeated context, artificial dependencies, duplicated work, unjustified MVP scope, and risk concentration. Propose a **minimal change set**; preserve accepted tasks, IDs, history, and stable references.

If the mode is not specified, choose CREATE when no plan exists; otherwise OPTIMIZE.

## Workflow

1. **Establish authority and scope.** Locate the current requirements, architecture, approved decisions, existing plan, and relevant repository state. Separate verified facts, assumptions, and proposals. If repository access is unavailable, say what is unverified.
2. **Identify outcomes and boundaries.** Map the behaviors required for the current milestone, mandatory cross-cutting constraints, and explicit exclusions. Surface missing business/architecture decisions without inventing them. Do not expand MVP scope.
3. **Build a candidate dependency graph.** Derive tasks from verifiable functional outcomes and necessary enabling foundations, not automatically from layers, classes, endpoints, or test categories. Prefer sequential execution when that is the user's workflow; retain genuine independent dependencies without inventing serial edges.
4. **Challenge task boundaries.** Apply the Merge, Split, Dependency, MVP, and Context-Reuse challenges in the planning standard. Balance repeated exploration/review overhead against blast radius, concurrency/security/data risks, and independent verification. Do not maximize task size merely to minimize task count.
5. **Order for safe delivery.** Put real prerequisites before consumers; favor early validation of high-impact uncertainty and useful end-to-end increments. Avoid large speculative scaffolding or future-proofing tasks.
6. **Evaluate the proposed plan.** Apply the quality gates. Highlight concrete risks, decisions for the human, and changes relative to an existing plan. Do not assign fabricated token/cost estimates; use qualitative reasoning unless measured data exists.
7. **Present for human approval.** Provide a compact task map with ID, deliverable, dependencies, risk, verification boundary, and rationale for the split. Include only consequential merge/split/dependency proposals, open decisions, and deferred work. **Do not update the repository unless explicitly requested.**
8. **After approval and authorization to write,** update only the approved plan and its necessary links/status references. Do not rewrite approved requirements or architecture, rename completed tasks, generate all future detailed TASK specifications, or implement work.

## Interaction and efficiency

- Inspect relevant files selectively; avoid exhaustive repository/doc scans without a concrete dependency.
- Reuse existing plan IDs and accepted decisions. Do not reopen approved architecture for preference alone.
- Use one concise rationale per non-obvious boundary, not repetitive explanations for every row.
- Treat exploration, verification, code review, and correction as normal phases of an implementation task. Create separate backlog tasks for them only when they have an independently useful outcome.
- Stop and ask for human decision if planning requires changing approved scope, policy, architecture, or security guarantees. Offer concrete options, trade-offs, and a recommendation.
- Do not fabricate source paths, task statuses, dependencies, test evidence, or implementation facts.
- Do not claim that a plan is optimal without comparative evidence. Prefer the simplest defensible decomposition.

## Output

1. **Task map** — ordered IDs, one observable deliverable each, dependencies, qualitative risk, and boundary rationale.
2. **Planning decisions** — approved constraints, decisions needed, and significant alternatives (only where material).
3. **Optimization notes** — proposed merges/splits/removals/dependency changes, with expected benefit and risk; for CREATE, only material boundary decisions.
4. **Deferred work** — items outside approved milestone, without treating deferral as an approved scope change.
5. **Readiness** — READY for task specification, NEEDS EXPLORATION, or BLOCKED, with concise evidence and human approval status.

The model proposes; the human approves the plan.
