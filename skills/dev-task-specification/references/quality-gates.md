# Specification Quality Gates

For each proposed task answer PASS / FAIL / N/A with a short reason.

1. **Evidence:** Are repository claims grounded in inspection? For greenfield, is absence of scaffold/database explicitly recognized?
2. **Problem:** Is the desired outcome stated independently of a preferred implementation?
3. **Atomicity:** Is there one cohesive deliverable and a bounded change? Would splitting create repeated context reconstruction without a meaningful independent benefit?
4. **Dependencies:** Do all prerequisites exist or appear earlier in the task map?
5. **Decisions:** Are binding business, architecture, and security choices human-approved rather than invented? Are unresolved implementation choices clearly delegated to explore?
6. **Boundaries:** Are allowed changes, forbidden changes, and relevant interfaces explicit?
7. **Invariants:** Are lifecycle, data, authorization, transaction and failure invariants recorded where relevant?
8. **Acceptance:** Can another engineer determine completion objectively?
9. **Tests:** Do scenarios include meaningful negative/edge/adversarial cases when relevant, and can they catch an incorrect solution?
10. **Verification:** Is there a feasible way to produce build/test/inspection evidence?
11. **Failure/rollback:** Are side effects, partial failure, idempotency and rollback covered where relevant?
12. **Architecture challenge:** Have relevant assumptions been tested, the simplest compliant approach considered, and materially better alternatives surfaced without speculative complexity?
13. **Handoff:** Are stop conditions, planning checkpoint, diff review, and human acceptance explicit?
14. **Explore focus and duplication:** Is there a concise, evidence-based starting focus for implementation explore, without repeated contracts or an artificial limit on necessary investigation?

### Decision rule
- A failed critical gate (1, 4, 5, 7, 8, 10) requires correction or explicit classification. BLOCKED is reserved for missing decisions/contracts that prevent safe progress; NEEDS EXPLORATION is for essential missing evidence. Implementation choices that can be investigated during execution explore do not automatically block READY.
- Other failures => revise before READY.
- Do not use a numeric score to override a critical failure.

### Anti-patterns
- "Build the whole backend" with no milestone deliverables.
- One task for entities, database, REST, workers, and AI.
- Calling a document implementation-ready while key semantics remain undecided.
- Assuming missing infrastructure already exists.
- Happy-path-only acceptance.
- Agent both invents domain policy and implements it.
- Tests written by the agent treated as sufficient proof of correctness.
- Unrelated cleanup disguised as part of the task.
- Treating a proposed technical approach as a binding contract without human approval.
- Requiring speculative recovery, concurrency, or abstraction mechanisms without concrete risks.
- Freezing architecture so tightly that execution explore cannot propose a better solution.
- Creating separate backlog tasks for routine exploration, verification, or correction phases without an independent outcome.
- Repeating the same requirements across multiple template sections.
