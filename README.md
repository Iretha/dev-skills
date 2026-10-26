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

## Workflow

Approved requirements and architecture → implementation plan → task specification → coding agent EXPLORE → **human approval** → IMPLEMENT + tests → independent REVIEW → findings analysis + **human decision** when needed → approved CORRECT as needed → **human acceptance**.

Planning owns overall task decomposition and dependencies. Specification owns detailed requirements for a single task and flags boundary problems without silently replanning. Execution and review remain separate; no skill may approve its own work.

The three original skills were initially copied from [java-dev-to-ai-systems-engineer](https://github.com/Iretha/java-dev-to-ai-systems-engineer) and verified byte-for-byte at migration time; the copies in this repository have since evolved. Keep existing consumers pointed at the old paths until their references are updated to this repository.
