# Development Skills

Reusable skills for AI-assisted software engineering.

**Principle:** THE MODEL PROPOSES; THE HUMAN DECIDES. Business behavior, architecture, risk acceptance, plan approval, and final task acceptance remain human-owned.

## Skills

| Skill | Responsibility |
| --- | --- |
| [dev-implementation-planning](skills/dev-implementation-planning/SKILL.md) | Create and optimize milestone implementation plans, task boundaries, dependencies, and execution order. |
| [dev-task-specification](skills/dev-task-specification/SKILL.md) | Specify one approved task with binding contracts, acceptance criteria, and verification expectations. |
| [dev-task-execution-prompt](skills/dev-task-execution-prompt/SKILL.md) | Generate phase-specific EXPLORE, IMPLEMENT, and CORRECT prompts for coding agents. |
| [dev-task-code-review-prompt](skills/dev-task-code-review-prompt/SKILL.md) | Generate independent, risk-based INITIAL and RE-REVIEW prompts. |
| [dev-code-review-analysis](skills/dev-code-review-analysis/SKILL.md) | Assess reviewer findings against evidence and approved contracts; propose dispositions for human approval without generating CORRECT prompts. |
| [dev-engineering-decision-support](skills/dev-engineering-decision-support/SKILL.md) | Analyze material engineering blockers and options against approved contracts; recommend human-owned decisions and provide concise post-approval handoff. |

## Workflow

Approved requirements and architecture → implementation plan → task specification → coding agent EXPLORE → engineering decision support when blocked → **human approval** → IMPLEMENT + tests → independent REVIEW → findings analysis + **human decision** when needed → approved CORRECT as needed → **human acceptance**.

Planning owns overall task decomposition and dependencies. Specification owns detailed requirements for a single task and flags boundary problems without silently replanning. Execution and review remain separate; no skill may approve its own work.

This repository is the maintained source of truth for these development skills. Historical copies in other repositories may be outdated; update consumers deliberately when changing their references.
