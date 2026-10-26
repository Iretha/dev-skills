---
name: agent-follow-up
description: Write minimal decision-delta or instruction-delta follow-up messages for an agent continuing in the same conversation. Preserve existing context, phase, and human approval boundaries without repeating task specifications or prior findings.
---

# Agent Follow-Up

## Purpose

Produce the **shortest complete actionable reply** to an agent that already has the task, repository, and conversation context. Communicate only newly approved decisions, clarifications, corrections, or next-step instructions. **THE MODEL PROPOSES; THE HUMAN DECIDES.**

This is a **message composition skill**, not a decision-making, task-planning, implementation, or review skill. Use the relevant architecture, engineering-decision-support, review-analysis, or execution skill to resolve substantive questions **before** composing the follow-up; do not rerun their analysis here.

## Preconditions

- The reply is going into the **same agent conversation** with intact context.
- The agent's current phase and the human's actual decision/authorization can be determined from the conversation.
- If either is unclear, ask only for the missing fact. Never infer authorization from agreement with a technical option.

If the agent is starting a **new session** or context has been lost, do not use delta-only mode: request or prepare a minimal context handoff using the applicable execution-prompt workflow.

## Composition rules

1. **Decision delta only.** State precisely what the human approved, rejected, clarified, or requested; include necessary changed constraints or acceptance implications.
2. **Reuse context.** Do not repeat TASK text, architecture, repo background, prior evidence, previous findings, test lists, or paths already known to the agent unless needed to disambiguate the new instruction.
3. **Preserve phase.** A clarification during EXPLORE authorizes continued exploration, **not IMPLEMENT**. A review clarification does not authorize code changes. Phase transitions (IMPLEMENT, CORRECT, push, PR, acceptance) require the human's explicit authorization and must follow the existing workflow.
4. **Respect ownership.** Do not make architectural/business/security decisions or expand scope; do not claim approval of unspecified options. If several questions were answered, relay each actual decision once without reopening settled topics.
5. **Avoid repeated work.** Tell the agent to continue from its existing findings and perform only the additional investigation, edits, or verification caused by the delta; retain mandatory verification and safety gates from the governing TASK/AGENTS.md.
6. **Stop conditions.** Escalate only a new material conflict, changed requirement, unsafe operation, or blocking evidence; do not require a fresh human decision for routine technical details within approved scope.
7. **Keep it short.** Usually 2–8 sentences or a few compact bullets. No boilerplate greeting, restated plan, duplicated contract, or generic checklist. Write in the agent's working language unless the human requests otherwise.

## Context continuity

After context compaction, reuse verified decisions and recover only missing or uncertain details rather than restarting the investigation. Continue in the existing session while relevant context remains reliable. If the context is lost or mostly irrelevant, use a concise new-session handoff through the task-execution workflow; a handoff never grants additional approval.

## Output

Return **only the copy-ready follow-up message** when the human asks for a prompt, unless a material ambiguity must first be resolved. Explicitly distinguish a decision from a phase authorization when both are present. Do not create files, commits, or change task status.
