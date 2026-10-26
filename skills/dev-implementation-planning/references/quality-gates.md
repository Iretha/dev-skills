# Planning Quality Gates

Apply PASS / FAIL / N/A with a short explanation only where a concern exists; do not generate a verbose gate report for an otherwise sound plan.

1. **Authority:** Are requirements, architecture, scope, and approved decisions correctly distinguished from proposals?
2. **Coverage:** Does the plan cover approved milestone outcomes without introducing future scope?
3. **Cohesion:** Does each task have a meaningful observable outcome rather than an arbitrary technical layer?
4. **Granularity:** Have both unnecessary microtasks and oversized risky tasks been challenged?
5. **Dependencies:** Are prerequisites real, acyclic, and traceable?
6. **Risk isolation and reviewability:** Are material data, security, destructive-operation, and concurrency risks appropriately bounded, and can an independent reviewer reasonably verify the diff?
7. **Verification:** Is each task's outcome independently testable or otherwise demonstrable?
8. **Context efficiency:** Have avoidable repeated exploration, review, and integration seams been considered without overriding correctness or risk isolation?
9. **Stability:** In OPTIMIZE, are DONE tasks, IDs, and references preserved, with minimal proposed edits?
10. **Human control:** Are decisions affecting business behavior, architecture, or MVP scope explicitly reserved for approval?

If evidence is insufficient, mark NEEDS EXPLORATION. If a human-owned decision prevents safe planning, mark BLOCKED. Do not treat an unresolved implementation detail as a blocker when it can be addressed in task Explore.
