# TASK-XXX — <Concise outcome>

**Type:** EXPLORE | DECIDE | IMPLEMENT | VERIFY | CORRECT  
**Status:** PLANNED | NEEDS EXPLORATION | BLOCKED | READY | DONE  
**Depends on:** TASK-... | None  
**Source of truth:** <links / approved decisions>

## Problem and desired outcome
<What problem exists and why this result matters>

## Deliverable
**One primary verifiable outcome:** <artifact or observable behavior>

## Evidence / existing state
- Verified facts:
- Inferences:
- Unverified assumptions:

## Human-owned decisions and invariants
- Confirmed:
- Invariants to preserve:
- Open decisions (if any):
- Exploration questions that do not block READY: <reference Implementation Explore Focus; do not duplicate>

## Architecture assessment
- Simplest compliant approach (proposal, not binding unless approved):
- Existing mechanisms to reuse:
- Material alternatives and trade-offs (only if warranted):
- Rejected alternatives and rationale (only if useful):
- Binding contracts vs implementation discretion: <reference approved decisions above rather than repeating them>

## Scope
**In:** ...
**Out:** ...
**Likely components:** ... (not mandatory file guesses)

## Implementation Explore Focus
- Relevant components / entry points (evidence-based, not exhaustive):
- Assumptions to validate:
- Open implementation questions (non-blocking):

## Preconditions
- ...

## Acceptance criteria
- [ ] Observable result 1
- [ ] Observable result 2

## Required scenarios
- Happy path:
- Edge/failure:
- Adversarial/security (if applicable):
- Concurrency/idempotency (if applicable):

## Verification and evidence
- Checks to execute:
- Evidence expected:
- Independent verification/review:

## Stop conditions
- Stop for conflicting source of truth, missing consequential decision, unsafe side effects, unapproved contract/scope changes, or impossible verification.
- Task-specific:

## Agent handoff
1. Read specification and inspect relevant repo state before implementation.
2. Independently validate the proposed approach against current code. Surface materially better alternatives and conflicts, distinguishing binding contracts from implementation suggestions. Produce a bounded plan and await human approval at the agreed checkpoint.
3. Implement only the approved scope.
4. Run required verification; report commands, results, limitations, and diff.
5. Human engineer reviews and accepts or requests bounded correction.

## Completion report
- Deliverable:
- Changed files / artifact links:
- Verification evidence:
- Deviations / remaining risks:
- Human acceptance: PENDING | ACCEPTED | REWORK
