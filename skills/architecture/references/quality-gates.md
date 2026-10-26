# Architecture Quality Gates

Apply proportionately to the system and requested mode. A gate may be NOT APPLICABLE; do not fabricate a risk to satisfy it.

1. **Authority** — requirements, constraints, approved decisions, and source-of-truth documents identified; unknown evidence labeled.
2. **Scope** — MVP inclusions/exclusions and business-policy ownership explicit; no silent scope expansion.
3. **Responsibilities** — component and data ownership, interactions, and state transitions sufficiently clear for current decisions.
4. **Contracts** — externally observable behavior and critical invariants coherent across applicable documents.
5. **Failure and security** — credible error, restart, concurrency, data-integrity, and trust-boundary risks addressed or explicitly deferred with impact.
6. **Simplicity** — no abstraction, infrastructure, or future capability without a present requirement or demonstrated benefit.
7. **Compatibility** — existing approved decisions, implementations, migrations, and protected task investment preserved; exceptions require human approval.
8. **Evidence** — findings and trade-offs supported by specific scenarios or sources; no invented verification.
9. **Decision ownership** — APPROVED versus PROPOSED/OPEN/DEFERRED clear; unresolved material choices block readiness.
10. **Handoff** — architecture is sufficient for planning at the current scope; no premature TASK breakdown, implementation, or unauthorized repository edits.

A review may conclude **no material findings**. Report only consequential issues and the minimal evidence needed to resolve uncertainty.
