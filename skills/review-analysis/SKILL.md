---
name: review-analysis
description: Evaluate an independent coding-agent review report against a task's approved contracts and concrete evidence. Classify meaningful findings, recommend human decisions, and prepare an approved correction scope without implementing code or generating a CORRECT prompt.
---

# Dev Code Review Analysis

## Purpose

Help the human decide what to do with findings from an independent code review. Assess **evidence and impact**, not the reviewer's confidence or finding count. Minimize avoidable correction cycles without dismissing real correctness, security, data, concurrency, or lifecycle risks.

**Human ownership:** The model proposes; the human decides whether to accept, reject, investigate, defer, or change a contract. This skill does not perform code review, edit code, merge branches, accept tasks, or generate coding-agent prompts. After approval, `task-execution` owns the CORRECT prompt.

## Inputs

- Review report with finding IDs, severity, location, scenario, and evidence.
- TASK specification and applicable approved contracts; relevant code/diff or verification evidence when available.
- Existing human decisions and prior correction/re-review history when relevant.

If direct code access is unavailable, do not claim independent verification; label the conclusion as provisional and request only the missing evidence needed to decide.

## Workflow

1. **Establish authority.** Separate approved business/architecture contracts, actual code evidence, reviewer assertions, and preferences. Read only relevant TASK sections and cited code; do not repeat the full implementation exploration.
2. **Assess each material finding.** Check whether the alleged scenario is reachable, whether guards or tests already cover it, and whether the impact violates a contract or presents a concrete meaningful risk. A sound static argument may suffice; reproduction is not mandatory. Do not invent certainty.
3. **Classify.** Use CONFIRMED, PLAUSIBLE—NEEDS EVIDENCE, NOT SUBSTANTIATED, or DESIGN/POLICY DECISION. Independently assess severity and blocking impact; do not automatically inherit reviewer labels. State the minimal evidence needed for unresolved findings.
4. **Recommend disposition.** For each finding propose FIX, INVESTIGATE, REJECT, DEFER (only with human risk acceptance), or ESCALATE for human architecture/business decision. Never silently accept risk or change binding contracts.
5. **Consolidate correction scope.** Group accepted findings by shared root cause or affected behavior where doing so reduces cycles without increasing risk. Preserve finding IDs and traceability. Recommend minimal fixes and focused regression evidence; identify mandatory impacted checks. Avoid unrelated refactors and speculative safeguards.
6. **Human checkpoint.** Present the compact assessment, disputed claims, proposed correction set, and decisions requiring approval. Stop; do not generate a CORRECT prompt until the human has approved the disposition. After approval, hand the accepted finding IDs, evidence, minimal correction boundaries, and required verification to `task-execution`.

## Efficiency and safety

- Prioritize Critical/High and material Medium issues; assess all consequential findings, without an arbitrary numeric cap or prolonged nit-hunting.
- No automatic rejection of a finding because tests pass; no automatic acceptance because the reviewer claims a defect.
- Do not reopen approved architecture for style or preference. Escalate concrete contract defects. Establish finding validity and whether a human-owned decision is needed here; delegate comparison of engineering/architecture options to `decision-support` rather than duplicating that analysis.
- Do not turn this analysis into a second independent full code review. Inspect only evidence needed to adjudicate reported findings or a directly implicated risk.
- Keep concise, auditable conclusions. One finding can be summarized in a few sentences when evidence is decisive.
- Re-review after correction belongs to `code-review`, not this skill.
- Treat AGENTS.md recommendations as nonblocking unless a concrete approved project rule is violated. Do not edit AGENTS.md.

## Output

A compact table or equivalent structured assessment:

| Finding | Assessment + evidence | Impact / severity | Proposed disposition | Minimal correction or evidence needed |
|---|---|---|---|---|

Then state:
- **Correction package:** accepted findings grouped by root cause, scope, and verification; no agent prompt.
- **Human decisions:** only outstanding approvals or meaningful trade-offs.
- **Readiness:** READY FOR HUMAN DECISION, NEEDS EVIDENCE, or BLOCKED BY CONTRACT DECISION.

Never mark the TASK DONE or claim a reviewer verdict constitutes human acceptance.

For a reply to an agent continuing in the same conversation, use `agent-follow-up` to communicate only the approved decision/instruction delta; do not duplicate task context or infer phase authorization.
