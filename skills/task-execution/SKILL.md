---
name: task-execution
description: Generate concise, phase-specific prompts for coding agents executing an existing, detailed dev task specification. Use for exploration, approved implementation, and bounded corrections. Does not write specifications or execute tasks.
---

# Task Execution Prompt

## Purpose

Produce a **copy-paste-ready, token-efficient prompt** for a coding agent working from an existing TASK specification. The TASK is the authoritative description of requirements, scope, acceptance criteria, and verification. **Do not restate it.**

This skill prepares prompts; it does not implement tasks or change task statuses. **It is a prompt-authoring skill for ChatGPT, not a prerequisite or instruction source for the coding agent. Never tell the coding agent to locate, install, read, or follow this skill.**

**Principle: Minimum sufficient context, full verification. The model proposes; the application decides; the human accepts.**

## Inputs

- TASK ID and task specification URL **or** repository-relative path (prefer the exact location supplied by the user).
- Repository URL when needed to disambiguate the checkout.
- Requested phase: `EXPLORE` (default), `IMPLEMENT`, or `CORRECT`.
- Prior agent findings and human decisions, when available in the conversation.
- Only task-specific constraints not already captured in the specification.

Do not search the whole repository just to compose a prompt. If the exact TASK location is unknown and repository access is available, locate it narrowly; otherwise ask for the path. Never invent a path, accepted status, approval, or test evidence.

## Context budget rules

1. **Reference, do not duplicate.** Point the agent at the TASK file. Do not copy its field lists, test cases, acceptance criteria, or architecture into the prompt.
2. **Read selectively.** Direct the agent to follow the TASK's references and inspect only relevant code, configuration, and tests. Avoid blanket instructions to read all docs or the entire implementation plan.
3. **Preserve source-of-truth hierarchy.** The TASK and its authoritative referenced contracts govern requirements; the actual repository governs current implementation facts. Surface conflicts rather than silently resolving them.
4. **No repeated exploration and minimal context handoff.** In later phases, reuse findings and approved decisions already in the agent's context; recheck only where changes or uncertainties require it. Prefer continuing the same session when its context is useful. If a new session is necessary, pass a concise handoff containing TASK ID/spec path, branch and current commit, approved decisions, completed work, remaining actions, verification commands/results (with commit applicability), and open blockers/risks. Link authoritative documents rather than copying them; omit failed hypotheses and verbose logs unless needed for a live issue. Do not create a separate persistent handoff document by default.
5. **Keep reports concise but auditable.** Report changed files, exact commands/results, failures, and risks without reproducing the TASK or narrating routine work.
6. **Do not trade correctness for tokens.** Never omit necessary tests, negative cases, security boundaries, human approval, or stop conditions. During implementation, run focused checks for fast feedback; before handoff, run every mandatory applicable verification gate. After corrections, rerun affected regressions and any other impacted mandatory checks. Capture verbose build/test output in local ignored logs when permitted; show concise status and relevant failure excerpts, retrieving full logs only as needed.
7. **Respect repository instructions.** Tell the agent to read applicable `AGENTS.md` files when present; never assume they exist or generate them automatically. The coding agent follows the generated prompt, repository instructions, TASK specification, and authoritative references—not this prompt-generation skill.
8. **Escalation to ChatGPT.** On conflicting contracts, missing consequential decisions, destructive changes, unapproved scope expansion, or unverifiable mandatory checks, stop the affected work. Report exact references, options and trade-offs, a recommendation, and a **self-contained prompt the human can paste into ChatGPT**. Resume only after human direction and rereading any updated authoritative documents.
9. **Per-task Git branch and review boundary.** For first IMPLEMENT, fetch latest `origin/main` and create a dedicated new branch for the TASK (for example `task-02-010-worker-infrastructure`). For explicitly approved resumption of the **same** task, first verify branch identity, base/history, worktree state, existing commits, and approved plan; safely continue the existing task branch without overwriting or resetting work. Never implement on `main` or reuse an unrelated task branch. Commit verified changes to that branch and push **only that branch** to `origin` for subsequent human/ChatGPT code review. Never push to `main`, merge, create or update a PR, or change task/plan statuses. PR creation is human-owned. Human review determines DONE. EXPLORE remains read-only, including no branch creation; CORRECT works on the existing task branch unless the human directs otherwise. If branch ownership, approval, uncommitted changes, or safe continuation is uncertain, stop and ask rather than resetting, rebasing, overwriting, or creating a conflicting branch.
10. **Architecture challenge during EXPLORE.** Validate the specification's proposed implementation against current code. Reuse existing mechanisms and propose materially better alternatives only with concrete evidence and trade-offs. Distinguish binding approved contracts from nonbinding proposals; do not reopen settled decisions for preference alone. Escalate any required contract change to the human.
11. **Risk-adaptive Explore and sufficiency.** Scale exploration depth to the task's uncertainty and consequences: narrow, well-specified local changes need focused inspection; unfamiliar integration or material migration, security, concurrency, and lifecycle risks warrant deeper investigation. End when change locations, proposed approach, verification, and material blockers are supported by sufficient evidence. Investigate remaining concrete risks, not hypothetical improvements. The explicit human approval gate applies at every depth.
12. **Bounded pre-commit self-review.** Before committing, compare the diff against the TASK acceptance criteria, approved scope, material risk scenarios, and test evidence. Fix concrete omissions; do not start a second architecture review or duplicate the independent reviewer.
14. **Base drift check.** At IMPLEMENT start or safe resumption, check relevant changes since EXPLORE/last approval. Reinspect only affected areas. Adapt routine implementation details within the approved scope and risk envelope; stop for renewed human approval if changes materially affect approach, scope, contracts, security/data/concurrency guarantees, or risk. Do not restart exploration by default.
15. **No speculative scaffolding.** Do not add AGENTS.md, frameworks, helper documents, or extra workflow files solely to save prompt tokens.

## Phase selection

### EXPLORE — default

Generate a short prompt that:
- Identifies the TASK by exact path and says to follow its requirements, references, acceptance criteria, and workflow.
- Requires targeted **read-only** inspection of relevant implementation and dependencies.
- Requests a concise, risk-proportionate plan: exact proposed files, important technical choices, test/verification approach, conflicts or open questions. Validate proposed architecture against current code and raise only evidence-backed improvements; preserve approved contracts.
- Forbids modifying files, running destructive operations, or updating task/status documents.
- **Stops for explicit human approval** before implementation.

Do not demand an exhaustive report of already-known stack details.

### IMPLEMENT — only after explicit human approval

Generate a short prompt that:
- Refers to the same TASK and the **approved plan already in context**.
- Includes only actual human-requested corrections/clarifications not already in that plan.
- Authorizes implementation **within the approved scope**.
- Requires focused checks during development, a bounded diff self-review against acceptance criteria and scope, and complete mandatory verification before handoff under the TASK's acceptance criteria, including relevant positive/negative tests, isolation, full applicable build, and diff review. Keep verbose logs in permitted ignored files and surface only relevant output unless more is needed.
- Requests concise evidence: branch name, base commit, pushed commit SHA, compare/review URL, changed files, exact commands and outcomes, failures/unverified checks, deviations, remaining risks.
- Requires a fresh dedicated task branch from updated `origin/main` on first implementation, or verified safe continuation of the same approved task branch on resumption; commit and push **only that branch** to `origin` for review; forbids pushing/merging into `main`, creating/updating PRs, or changing TASK specs and central execution statuses.
- Stops for human review/acceptance. Never claim human acceptance from test success. On blockers, return the ChatGPT-ready clarification prompt described above.

If no approval is evident, generate an EXPLORE/approval-request prompt instead; do not silently authorize implementation.

### CORRECT — bounded repair after review

Generate a short prompt that:
- Names the specific observed defect or failed criterion, using the user's supplied evidence.
- Restricts edits to the minimal affected area, retaining the approved TASK scope.
- Requires targeted regression checks and other impacted mandatory checks, using concise diagnostic output and permitted ignored logs for verbose output.
- Requests changed files, commands/results, residual risks.
- Uses the existing task branch and pushes verified correction commits only to that branch for re-review; never pushes to `main`. If the correction changes scope or contract, stop for approval first.

## Output format

- Return **one** directly copyable English prompt, unless the user asks for another language or multiple variants.
- Keep it as short as reasonably possible; generally 80–160 words for EXPLORE and shorter for uncomplicated IMPLEMENT/CORRECT.
- Include the TASK URL or path and explicit phase/stop gate.
- **Do not include any instruction to read or follow `task-execution` or any external prompt-authoring skill.** Its rules must be translated into the generated prompt itself.
- Do not prepend a second specification, long explanation, or duplicated checklist.
- If a critical missing detail prevents a safe prompt, ask one focused question.

## Default EXPLORE prompt

```text
Work on TASK-NNN:
<exact TASK specification URL or repository-relative path>

Read applicable AGENTS.md instructions when present. Follow the TASK specification, its authoritative references, acceptance criteria, and agent workflow.

Phase: read-only exploration and planning. Scale investigation to concrete uncertainty and risk; keep well-specified local changes focused, and investigate material migration, security, concurrency, lifecycle, or unfamiliar integration risks more deeply. Inspect only relevant code, configuration, tests, and referenced documentation. Reuse established conventions; validate the proposed architecture against current code, and identify evidence-backed better alternatives, conflicts, missing prerequisites, or decisions needing approval. Preserve binding approved contracts; do not reopen decisions for preference alone.

Return a concise plan with exact proposed files, key technical decisions, verification approach, and unresolved risks. Do not repeat the specification or unchanged project context. Stop once change locations, approach, verification, and material blockers are sufficiently established.

Do not modify files, run destructive operations, or change task/status documents.

If blocked, provide exact references, options, a recommendation and a self-contained ChatGPT discussion prompt. Do not push, merge, or create/update a PR during EXPLORE.

STOP and wait for explicit human approval before implementation.
```

## Default IMPLEMENT prompt

```text
Approved. Implement TASK-NNN (<exact TASK specification URL or path>) according to the agreed plan and task specification. Read applicable AGENTS.md instructions when present.

Apply only these additional clarifications: <omit if none>.

Diagnose failures before broad reruns; distinguish introduced regressions from pre-existing or uncertain failures, and avoid unrelated fixes. Run focused checks while developing, then all mandatory applicable verification before handoff. Before committing, briefly self-review the diff against acceptance criteria, scope, material risks, and test evidence; avoid a second full architecture review. Save verbose output to permitted ignored logs and inspect relevant failure excerpts first; do not hide failures. Report changed files, exact commands and results, failures or unverified checks, deviations, and remaining risks.

On first implementation, fetch latest origin/main and create a dedicated TASK branch from it. If resuming this same approved task, verify branch identity, history, worktree, existing work, and approval before safely continuing its branch; never reset or overwrite work. Recheck only changes relevant since EXPLORE/approval. Adapt routine technical details within approved scope; stop for renewed approval if approach, scope, contracts, material risks, or security/data/concurrency guarantees change. If branch ownership or safe continuation is uncertain, stop and ask. Implement and verify on that branch, commit verified changes, and push only the task branch to origin for code review. Never push to main, merge, or create/update a PR. The human owns PR creation.

Report the branch, base SHA, pushed commit SHA, compare URL, changed files, and verification evidence. Do not change task specifications or execution statuses. STOP for human review and acceptance.
```

## Default CORRECT prompt

```text
Correct the following verified issue in TASK-NNN: <specific issue and evidence>.

Keep changes within the approved scope; stop for approval if a contract or scope change is necessary. Diagnose failures before broad reruns. Run targeted regression tests and any impacted required checks. Keep verbose logs in permitted ignored files and inspect relevant excerpts first. Report the diff, commands/results, and remaining risks.

Use the existing TASK branch; commit verified corrections and push only that branch to origin for re-review. Never push to main, merge, or create/update a PR. The human owns PR creation. If blocked, provide a self-contained ChatGPT discussion prompt.

Report branch, pushed commit SHA, compare URL and verification evidence. Do not change task specifications or execution statuses. STOP for human re-review.
```

For a reply to an agent continuing in the same conversation, use `agent-follow-up` to communicate only the approved decision/instruction delta; do not duplicate task context or infer phase authorization.
