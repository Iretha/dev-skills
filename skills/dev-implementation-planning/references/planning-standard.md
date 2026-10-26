# Implementation Planning Standard

## Task boundary

One task delivers one **cohesive, independently verifiable outcome**. A task may change entities, migrations, repositories, services, APIs, and tests together when they jointly deliver that outcome. Do not split by technical layer by default. Avoid tasks so large that failures cannot be localized, reviewed, or safely corrected.

Correctness, risk isolation, and reviewability take precedence over token savings. Sharing components or context does not alone justify combining tasks with different failure modes or an unreviewable diff.

## Five mandatory challenges

1. **Merge:** Would combining related tasks eliminate repeated context reconstruction, integration seams, or agent cycles without materially increasing risk or losing independent verification? If yes, propose merging.
2. **Split:** Does a task combine independently meaningful outcomes or materially different risk boundaries (e.g. destructive cleanup, fencing, security, migrations)? If splitting improves isolation, testability, or review, propose it.
3. **Dependency:** Is each edge a true prerequisite? Remove artificial ordering. Do not infer parallel execution merely because tasks are independent.
4. **MVP:** Is each outcome required by approved current scope? Propose deferral of nonessential work, but obtain human approval before changing scope.
5. **Context reuse:** Will adjacent tasks repeatedly require the same difficult code/contracts? Prefer cohesive boundaries or a sequence that preserves understanding, unless risk isolation outweighs that benefit.

## Planning heuristics

- Prefer thin, working vertical increments to broad scaffolding or layer-by-layer tickets.
- A foundation task is justified when multiple outcomes depend on it or when it isolates a significant technical risk and can be verified on its own.
- Do not turn ordinary EXPLORE, VERIFY, REVIEW, or CORRECT phases into separate backlog tasks.
- Do not manufacture tasks for speculative resilience, extensibility, or defensive mechanisms absent an approved requirement or concrete risk.
- Preserve explicit contracts and data lifecycle invariants; plan verification for negative/failure cases where relevant.
- Place high-risk uncertainty early enough to avoid expensive rework, but do not implement unresolved policy.
- Qualitative risk: LOW / MEDIUM / HIGH, with a concrete reason; avoid arbitrary numeric complexity scores.
- Cost optimization is multi-objective: repeated context, implementation effort, test/review overhead, integration risk, and expected correction cycles. Do not optimize only task count.
- Keep stable task IDs; in OPTIMIZE mode, do not silently reassign IDs, change DONE tasks, or break existing references.

## Ownership and handoff

Planning readiness (READY FOR SPECIFICATION) means the approved task boundary is clear enough to write a detailed specification; it does not mean the TASK is READY for coding-agent EXPLORE. Execution status remains project-owned. Each approved plan entry passes stable ID, deliverable, real dependencies, scope boundary, authoritative contract references, risk focus, and verification boundary to specification without a separate artifact.

The human approves business/architecture decisions, risk acceptance, and plan changes. Planning agent may recommend alternatives with consequences. Task-specification skill owns detailed acceptance criteria, test scenarios, and per-task handoff; planning skill should give a clear verification boundary but not duplicate full specifications.
