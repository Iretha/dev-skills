# Coding Agent Task Standard

## Atomicity
One task = one primary independently observable deliverable. Multiple code files are acceptable when needed for one vertical behavior. Split when distinct outcomes can be built, reviewed, and verified separately. Do not split solely by technical layer if doing so creates nonfunctional fragments without a useful verification boundary. Avoid micro-tasks that increase explore and implementation overhead without reducing delivery risk. Prefer cohesive vertical slices when splitting would repeatedly reconstruct the same context. Split only for a meaningful independent deliverable, dependency, risk boundary, or verification benefit.

## Task types
- **EXPLORE:** read-only investigation; deliverable is evidence report, dependency map, conflicts and decisions.
- **DECIDE:** human-reviewed options and recorded decision; no implementation.
- **IMPLEMENT:** bounded code/config/migration change plus tests and evidence.
- **VERIFY:** independent scenario/test/review report without feature implementation.
- **CORRECT:** bounded repair against a documented acceptance failure.

Routine EXPLORE, DECIDE, VERIFY, and CORRECT activities are phases of an implementation task by default, not automatically separate backlog tasks. Create dedicated tasks of these types only when they produce a distinct, independently useful outcome.

## Minimum contract
Each task must specify ID, type, status, problem, one deliverable, source of truth, prerequisites, in/out scope, relevant invariants, acceptance criteria, verification evidence, and stop conditions. Optional sections must be added when risk warrants: data migration, authorization, concurrency, idempotency, transaction boundary, failure behavior, side effects, monitoring, compatibility, rollback.

## Dependency and readiness
A task is READY when its outcome, approved constraints, scope, and prerequisite path are clear enough for a safe read-only implementation explore. Implementation choices and explicitly labeled exploration questions may remain open. BLOCKED applies when a missing human-owned policy or conflicting binding contract prevents meaningful safe exploration or implementation approval. A greenfield task must not reference nonexistent infrastructure as if implemented. Distinguish `PLANNED`, `NEEDS EXPLORATION`, `BLOCKED`, `READY`, `DONE`. `DONE` requires human acceptance, not just an agent claim.

## Context efficiency
State each binding contract once and refer to it rather than repeating it across sections. Provide a brief Implementation Explore Focus: relevant components supported by evidence, assumptions requiring validation, and open implementation questions. Do not prescribe an exhaustive file list or constrain investigation when new risks emerge.

## Architectural alternatives
During specification, challenge assumptions against available evidence. Prefer the simplest compliant solution and reuse existing mechanisms where appropriate. Compare materially different alternatives only when there is a concrete trade-off. Separate binding decisions/invariants from nonbinding proposed approaches; record important rejected alternatives and reasons. The execution agent independently validates the proposal against current code and can recommend changes for human approval.

## Engineering ownership
Human owns problem framing, policy, architecture, permissions, risk acceptance, plan approval, and final diff acceptance. Agent may research, propose, implement within approved scope, test, and report. No silent expansion of scope.

## Acceptance criteria
Use observable outcomes; cover positive and negative cases. Require tests that could fail on an incorrect implementation. Include security/tenant boundaries, retries, concurrency, rollback and adversarial cases only when relevant. Verification must include evidence independent of self-reported success where practical.

## Stop/escalation
Stop for contradictory sources of truth, missing business/architecture/security policy, unexpected public contract changes, destructive operations, unverifiable requirements, inability to run mandatory checks, or material scope growth. Record the blocker and options; do not guess.
