# Architecture Standard

## Scope and evidence

- Start from goals, actors, use cases, constraints, MVP boundaries, quality attributes, and existing approved contracts. Requirements may be incomplete: surface only gaps that affect a concrete decision.
- For existing systems, distinguish actual code behavior from intended and approved contracts. Cite exact repository evidence when claiming a current mechanism or conflict.
- Preserve existing investment: avoid changing approved architecture, implemented interfaces, applied migrations, and specified/started tasks for preference alone. Escalate material incompatibilities and document the approved migration path.

## Design principles

- Prefer the smallest architecture satisfying today's approved scope; explicitly defer speculative extensibility.
- Establish clear ownership of data, state transitions, side effects, and cross-component responsibilities.
- Define externally observable contracts and invariants before internal implementation details.
- Address only relevant operational dimensions: authentication/authorization, trust boundaries, data retention/integrity, concurrency/atomicity, retries/idempotency, partial failures, recovery, observability, resource limits, and deployment constraints.
- Avoid unsupported absolutes: a monolith, modular monolith, microservices, synchronous calls, messaging, relational persistence, or native SQL is a choice requiring context, not a default dogma.
- Keep business policy human-owned. Never treat a technical convenience as approval to change semantics or security guarantees.

## Decision discipline

- For each consequential choice, state: question, known constraints, credible options (one is enough when there is no real alternative), recommended option, material costs/risks, and decision owner.
- Status vocabulary: APPROVED (explicitly accepted), PROPOSED (recommended but not accepted), OPEN (needs resolution), DEFERRED (consciously postponed with trigger/impact).
- Approved decisions remain binding until the human changes them. Capture why a non-obvious choice was made to avoid repetitive debate.
- Group related questions, but discuss dependent decisions in order; avoid large up-front questionnaires.

## Review and evolution

- Validate requirement coverage and internal consistency, not conformity to a favorite architecture style.
- Identify concrete failure scenarios and contract contradictions; classify blockers separately from optional hardening.
- For evolution, assess backward compatibility, existing data/migrations, integration consumers, rollout and verification implications.
- Avoid producing new tasks, broad rewrites, or duplicated canonical contracts as a side effect of architecture work.
