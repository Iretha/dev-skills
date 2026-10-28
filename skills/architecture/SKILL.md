---
name: architecture
description: Collaboratively design, review, evolve, and check consistency of software architecture from requirements, constraints, approved decisions, and repository evidence. Supports DESIGN, REVIEW, EVOLVE, and CONSISTENCY modes with human-owned decisions and risk-proportionate investigation.
---

# Software Architecture

## Purpose and boundary

Help a human architect define **system behavior, component responsibilities, interfaces, data semantics, operational guarantees, and binding contracts** before implementation planning. Work interactively; **THE MODEL PROPOSES; THE HUMAN DECIDES**. Start from incomplete requirements when necessary: identify material gaps and clarify them, but do not replace product/business analysis or invent business policy.

This skill does **not** create implementation task breakdowns, TASK specifications, code, or coding-agent prompts; it does not approve decisions. `implementation-planning` owns task decomposition after architecture approval. `decision-support` owns a narrow blocker arising inside an already-running task; use this skill for system-level design, evolution, and cross-contract coherence.

Read [architecture standard](references/architecture-standard.md) and [quality gates](references/quality-gates.md). Use [architecture template](templates/architecture.md) only for sections applicable to the system; preserve the repository's canonical document structure rather than forcing a new one.

## Modes

- **DESIGN** — establish an architecture for a new system or milestone from goals, constraints, and known requirements.
- **REVIEW** — independently challenge an existing architecture for substantiated gaps, risks, unnecessary complexity, and requirement mismatches.
- **EVOLVE** — add or change capabilities while preserving approved contracts and existing investment; propose a minimal compatible change set.
- **CONSISTENCY** — trace approved decisions across requirements, architecture, canonical contracts, and scope; identify actual contradictions or missing authority.

Select the narrowest mode matching the request; ask only when the intended outcome cannot be inferred. Do not automatically perform a full review after every small decision.

## Interactive workflow

1. **Establish authority and scope.** Locate relevant requirements, MVP boundary, existing architecture/contracts, approved decisions, constraints, and (for brownfield systems) only relevant code and tests. Separate verified facts, assumptions, proposals, and unresolved questions. If sources are unavailable, state what remains unverified.
2. **Clarify consequential requirements.** Identify behaviors, actors, integrations, quality attributes, operating assumptions, and failure expectations that materially affect architecture. Ask focused questions in dependency order; do not manufacture business requirements or demand complete requirements documentation before useful design discussion.
3. **Propose the simplest compliant design.** Describe boundaries, responsibilities, data ownership/flows, APIs/events, persistence, lifecycle, failure handling, and security as applicable. Reuse existing mechanisms where fit is evidenced. Avoid speculative abstractions, infrastructure, or future-proofing.
4. **Learn selectively from established solutions.** For a consequential uncertain design choice, inspect relevant framework guidance, mature open-source implementations, or comparable systems when useful. Identify the problem, scale, and constraints behind their approach. State **what we learned**, **what is justified for current requirements**, and **what we intentionally omit** because its complexity belongs to another scale or maturity level. Prefer extracting a small proven principle over copying architecture or infrastructure. Keep research proportional; do not require external comparisons for routine choices or treat a mature system's design as automatically suitable.
5. **Discuss one coherent decision topic at a time.** Present the decision, credible alternatives only when they exist, concrete trade-offs, a recommendation, and the exact human approval needed. Support follow-up questions in the same discussion. Do not bundle dozens of unrelated questions or treat a recommendation as approval.
6. **Record decision state.** Track **APPROVED**, **PROPOSED**, **OPEN**, and **DEFERRED** with rationale, scope, and affected canonical contracts where useful. Never infer APPROVED from silence. Preserve approved decisions and historical investment; reopen only for concrete contradictions, changed requirements, or material risks.
7. **Challenge risks proportionately.** Check applicable invariants, trust boundaries, data integrity, concurrency, lifecycle, partial failures, retries/idempotency, observability, deployment, and recovery. Spend depth where impact/uncertainty warrants it; stop investigating hypothetical edge cases with no credible scenario.
8. **Run an explicit, bounded gap analysis (REVIEW).** Trace material MVP requirements to architectural responsibilities, contracts, and guarantees. Identify missing decisions, contradictions, ownership gaps, and credible failure scenarios; distinguish blockers from explore-time validation and consciously deferred improvements. Do not manufacture gaps to fill a checklist. For other modes, apply a proportional consistency check.
9. **Assess simplification (REVIEW).** For material complexity-driving mechanisms, ask: which current requirement justifies this; can existing infrastructure satisfy it; is a simpler design behaviorally equivalent; and what guarantee is lost by removing or deferring it? Recommend **KEEP / SIMPLIFY / REMOVE / DEFER** only when supported by evidence and concrete trade-offs. Do not reopen approved decisions for style preferences or force simplification findings when none exist.
10. **Human checkpoint and documentation.** Present the concise current design, approved decisions, remaining blockers, material trade-offs, and verification implications. **Do not write repository files unless explicitly authorized.** After authorization, update only affected canonical architecture/contracts and necessary links; do not silently alter approved requirements, MVP, task IDs, specs, or implementation plan. Hand off to implementation planning only when the human approves architecture readiness.

## Efficiency

- Use topic-scoped exploration and source links; avoid repeated whole-repository/document reads and re-explaining settled decisions.
- In REVIEW/CONSISTENCY, report evidence-backed findings with location, scenario/impact, and smallest viable remedy. A clean result is acceptable.
- In REVIEW, make both **Gap Analysis** and **Simplification Assessment** visible in the outcome, even when either has no material findings. Organize relevant findings as **Requirements Gaps**, **Contract Consistency**, **Reliability & Security**, **Overengineering**, and **Deferred Improvements**; omit empty categories except for a concise explicit no-findings statement. Classify blockers separately from explore-time questions and future improvements. Do not turn these headings into mandatory findings or a long report.
- In EVOLVE, inventory protected decisions, implemented interfaces, migrations, and existing plans/specs before proposing changes. Prefer additive compatible changes; material exceptions need human approval.
- Do not generate one ADR per decision by default. Record concise decisions in existing canonical documents; create separate ADRs only when the repository convention or human explicitly requires them.
- Do not create a new architecture file if an authoritative one already exists. Do not turn the architecture into a class-by-class implementation plan.
- If a task-specific blocker is the only question, route to `decision-support` instead of invoking a broad architecture review.

## Output

Return only what advances the current discussion: current topic, verified constraints, recommended decision with material trade-offs, and precise question for human approval. For a requested complete architecture artifact, use the relevant sections of the template, marking unresolved decisions explicitly. End with readiness status: **READY FOR IMPLEMENTATION PLANNING**, **NEEDS DECISIONS**, or **NEEDS EVIDENCE**. Readiness is advisory, never automatic human approval.
