---
name: dev-task-code-review-prompt
description: Generate concise prompts for an independent, pragmatic, read-only review of a completed coding task branch against main, its specification, contracts, and project conventions. Supports focused re-review after corrections.
---

# Dev Task Code Review Prompt

## Purpose

Generate a copy-paste-ready prompt for a **separate review agent** to inspect an implemented task branch. Review for **correctness and meaningful risk, not perfection**. Report every substantiated issue that matters, but do not manufacture work.

This skill generates review prompts; it does not perform the review, change files, or accept tasks. **The model proposes; the human decides.**

## Inputs

- Repository URL, TASK ID, and exact task specification path or URL.
- Task branch and base branch (default `main`); prefer the exact pushed commit SHA if known.
- Review mode: `INITIAL` (default) or `RE-REVIEW`.
- For re-review: prior findings and correction commit/range.

Do not invent branch names, status, acceptance, or verification evidence. Ask one focused question if an essential identifier is missing.

## Independent review boundary

1. The reviewer must be independent of the implementing agent's reasoning or self-assessment. Inspect the **actual pushed branch diff against the appropriate main base**, not just the implementation summary.
2. Read applicable `AGENTS.md`, the task specification, referenced authoritative contracts, and only the relevant neighboring code/tests needed to validate the change. Do not audit the entire repository. Identify risks from the actual diff and investigate each material risk to sufficient confidence. Expand only for concrete suspicions or missing evidence; avoid redundant investigation.
3. **Read-only:** no edits, commits, pushes, merges, PRs, status updates, or changes to `AGENTS.md`. Running safe verification checks is allowed when practical; report which were actually run versus inferred from code.
4. Prioritize the actual change's risk profile, then evaluate applicable correctness, acceptance criteria, security, concurrency, transactions, failure handling, and test adequacy. Follow cross-cutting risks when relevant; avoid mechanical checklists.
5. Check explicit `AGENTS.md` rules and demonstrable existing project conventions, including applicable persistence, logging, error handling, testing, and architectural practices. Do not mistake personal preferences for conventions.
6. Do not demand stylistic rewrites, speculative abstractions, unrelated refactors, hypothetical edge-case coverage, or additional tests without a specific risk. Do not treat native SQL as inherently defective when justified.
7. **No numerical cap on findings.** Report all credible Critical/High issues; report Medium issues when tied to a concrete meaningful risk. Ignore Low/style-only nits unless they reveal a systemic, consequential problem. Do not keep searching for ever-smaller findings after the relevant diff and risks have been covered.
8. Before reporting a finding, check whether existing guards, contracts, or tests invalidate the suspected scenario. A convincing static argument can suffice without a reproducer. For each finding provide severity, location, concrete scenario, impact, and minimal correction. Medium findings require meaningful behavioral, contract, or maintainability risk, not design preference. Clearly distinguish verified from suspected issues; do not assert unsupported failures.
9. Separate **Code Findings**, **Convention Compliance**, and **AGENTS.md Recommendations**. Default to no `AGENTS.md` recommendations. Suggest a non-blocking rule only when an issue already found reveals a recurring or systemic risk with broad future usefulness; include proposed wording and evidence. Do not conduct a separate rule-hunting pass. Never modify the file.
10. Verdict is **Changes required** only for substantiated blocking issues; otherwise **Ready for human acceptance**. This is advice, never automatic acceptance or permission to merge.
11. After fixes, **re-review only corrected findings and immediately impacted code**, plus any newly evident regression. Verify the specific fix and relevant test evidence; do not restart a full review or architectural investigation unless the correction exposes a material new risk.
12. **Approved architecture boundary.** Review approved architectural decisions for correctness and contract compliance, not personal design preference. Challenge a binding decision only when concrete evidence shows a material defect or conflict; escalate rather than silently replacing it.
13. **Proportional verification.** Independently assess implementer test evidence and run targeted checks when they materially increase confidence. Do not automatically rerun the full suite, but run it when a concrete risk warrants it.
14. If review cannot be completed, identify the missing evidence and limit the verdict accordingly; do not invent certainty.

## Output format

Return one concise, directly copyable English prompt unless another language is requested. Refer to exact TASK and branch; avoid repeating the specification. The generated prompt should ask for a compact review report:

- **Code Findings** — blocking and non-blocking, with evidence and minimal fixes; explicitly state when none.
- **Convention Compliance** — material violations or compliant, with references.
- **AGENTS.md Recommendations** — only broadly reusable improvements, with proposed wording; otherwise none.
- **Verification** — checks run and not run.
- **Verdict** — Changes required / Ready for human acceptance / Unable to verify.

## Default INITIAL prompt

```text
Independently review TASK-NNN (<exact task specification URL/path>) in <repository>, branch <task-branch> against origin/main (commit <SHA if known>).

Review the actual branch diff using a risk-based approach, investigating material risks to sufficient confidence without redundant sweeps. Read applicable AGENTS.md, task acceptance criteria, authoritative referenced contracts, and only relevant adjacent code/tests. Expand only for concrete suspicions; respect approved architecture unless evidence reveals a material defect. Remain strictly read-only: no edits, pushes, merges, PRs, or status changes.

Focus on substantiated correctness, security, concurrency, transactional, failure-handling, acceptance-criteria, and material project-convention issues. Check existing guards, contracts, and tests before asserting a suspected failure. Report all substantiated meaningful findings without a numerical cap, each with severity, exact location, concrete scenario/impact, and minimal correction. Do not repeat sweeps in search of minor issues. Do not chase style, speculative improvements, or extra tests without a specific risk.

Return: (1) Code Findings, (2) Convention Compliance, (3) AGENTS.md recommendations only for recurring/systemic issues already evidenced in findings; otherwise none, (4) verification actually performed, using targeted independent checks when useful rather than automatically rerunning the full suite, (5) verdict: Changes required / Ready for human acceptance / Unable to verify.

Do not modify AGENTS.md. The human decides acceptance. STOP after the review.
```

## Default RE-REVIEW prompt

```text
Re-review TASK-NNN on <task-branch> after correction commit <SHA/range>. Recheck the previously reported findings, the correction diff, immediately impacted behavior/tests, and relevant verification evidence only. Do not restart architecture analysis unless a material new risk emerges. Remain read-only.

For each prior finding state resolved/unresolved with evidence. Report any newly introduced material regression or material convention violation, without style nitpicks or a full new audit. Recommend AGENTS.md changes only for systemic issues already evidenced by the review; otherwise none.

Report verification performed and verdict: Changes required / Ready for human acceptance / Unable to verify. Human acceptance remains separate. STOP.
```

For a reply to an agent continuing in the same conversation, use `dev-agent-follow-up` to communicate only the approved decision/instruction delta; do not duplicate task context or infer phase authorization.
