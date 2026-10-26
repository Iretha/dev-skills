# Development Skills

Reusable skills for AI-assisted software engineering.

**Principle: THE MODEL PROPOSES; THE HUMAN DECIDES.** The human owns business behavior, architecture, risk acceptance, plan approval, phase transitions, and final task acceptance.

## Quick start — ChatGPT shortcuts

In this ChatGPT workflow, you can **ask** for a skill by its slash-style alias (or by the uppercase code without a slash). These are **documented conversational shortcuts, not registered ChatGPT slash commands**: they do not install or automatically load a skill. The assistant should resolve the alias to the linked `SKILL.md` and follow it; if the skill cannot be accessed, it should say so rather than claim it was applied.

| Shortcut | Code | Skill (current repository path) | Typical request |
| --- | --- | --- | --- |
| `/arch` | `ARCH` | [dev-software-architecture](skills/dev-software-architecture/SKILL.md) | `/arch review Stage 2` |
| `/plan` | `PLAN` | [dev-implementation-planning](skills/dev-implementation-planning/SKILL.md) | `/plan optimize Stage 3` |
| `/spec` | `SPEC` | [dev-task-specification](skills/dev-task-specification/SKILL.md) | `/spec TASK-02-042` |
| `/exec` | `EXEC` | [dev-task-execution-prompt](skills/dev-task-execution-prompt/SKILL.md) | `/exec explore TASK-02-025` |
| `/review` | `REVIEW` | [dev-task-code-review-prompt](skills/dev-task-code-review-prompt/SKILL.md) | `/review initial TASK-02-025` |
| `/analyze` | `ANALYZE` | [dev-code-review-analysis](skills/dev-code-review-analysis/SKILL.md) | `/analyze` (review report above) |
| `/followup` | `FOLLOWUP` | [dev-agent-follow-up](skills/dev-agent-follow-up/SKILL.md) | `/followup` (approved decisions above) |
| `/decide` | `DECIDE` | [dev-engineering-decision-support](skills/dev-engineering-decision-support/SKILL.md) | `/decide` (agent blocker above) |

**Syntax:** `/<shortcut> [mode] [target or instruction]`, or `CODE [MODE] [target or instruction]`. Mode names are case-insensitive. Omit a mode when the intended action is clear or the skill defines a default; omit a TASK ID when the current conversation already identifies it. A shortcut is a request to use a skill, **not** authorization to edit repositories, implement code, advance a phase, push, merge, or mark work accepted.

## Skills in detail

### 1. Architecture — `/arch` / `ARCH`

**Skill:** [dev-software-architecture](skills/dev-software-architecture/SKILL.md)

**Use for:** Designing or challenging system-level architecture: component boundaries, data ownership, APIs, lifecycle, failures, concurrency, security, operational guarantees, and consistency with approved requirements. The human decides architectural trade-offs. **Not for** splitting work into TASKs or resolving a narrow implementation blocker that already has an approved architecture.

| Mode | When to use | Example |
| --- | --- | --- |
| `DESIGN` | Design a new system or milestone from goals and constraints. | `/arch design Stage 3` |
| `REVIEW` | Find evidence-backed architectural gaps, risks, or unnecessary complexity. | `/arch review Stage 2` |
| `EVOLVE` | Extend approved architecture while protecting existing contracts and investment. | `/arch evolve add a new municipality` |
| `CONSISTENCY` | Check requirements, architecture, and canonical contracts for contradictions. | `/arch consistency Stage 2` |

**Produces:** Focused recommendations and decision points; optionally an approved architecture/document update when separately authorized. **Does not approve its own proposals.**

### 2. Implementation planning — `/plan` / `PLAN`

**Skill:** [dev-implementation-planning](skills/dev-implementation-planning/SKILL.md)

**Use for:** Turning approved architecture and requirements into an ordered implementation plan with cohesive tasks, genuine dependencies, risk boundaries, and verification scope. **Not for** detailed TASK specifications or coding.

| Mode | When to use | Example |
| --- | --- | --- |
| `CREATE` | Create a plan where none exists. | `/plan create Stage 3` |
| `OPTIMIZE` | Improve an existing plan without casually changing completed, started, or specified tasks. | `/plan optimize Stage 2` |

**Default:** `CREATE` if no plan exists; otherwise `OPTIMIZE`. **Produces:** Proposed task map, dependencies, trade-offs, and planning readiness. Human approves the plan.

### 3. Task specification — `/spec` / `SPEC`

**Skill:** [dev-task-specification](skills/dev-task-specification/SKILL.md)

**Use for:** Writing **one** implementation-ready TASK specification from an approved plan entry, with scope, contracts, acceptance criteria, risks, and verification expectations. Also use it to assess a draft TASK's readiness. **Not for** changing the overall plan or implementing the task.

**Modes:** No formal named modes in the current skill. The requested operation determines the work:

- **Specify:** `/spec TASK-02-042` — draft or update the specified TASK from its approved plan entry.
- **Check readiness:** `/spec review TASK-02-042` — review completeness and material blockers; `review` here is a request description, **not a formal skill mode**.

**Produces:** One TASK specification and readiness assessment (`READY`, `BLOCKED`, or `NEEDS EXPLORATION`). Writing to the repository requires explicit authorization.

### 4. Coding-agent execution prompts — `/exec` / `EXEC`

**Skill:** [dev-task-execution-prompt](skills/dev-task-execution-prompt/SKILL.md)

**Use for:** Creating **copy-ready prompts** for a coding agent working from an existing TASK specification. This skill writes prompts; it does **not** implement code.

| Phase / mode | When to use | Example |
| --- | --- | --- |
| `EXPLORE` | Read-only investigation, proposed approach, risks, and tests before human approval. | `/exec explore TASK-02-025` |
| `IMPLEMENT` | After **explicit** approval of the implementation approach. | `/exec implement TASK-02-025` |
| `CORRECT` | Prepare a bounded correction prompt for approved issues. | `/exec correct TASK-02-025` |

**Default:** `EXPLORE`. **Produces:** One phase-specific agent prompt referencing the TASK rather than repeating its content. Selecting a phase in the request does not waive any required human approval or Git safety boundary.

### 5. Independent code-review prompts — `/review` / `REVIEW`

**Skill:** [dev-task-code-review-prompt](skills/dev-task-code-review-prompt/SKILL.md)

**Use for:** Generating prompts for a **separate, read-only review agent** to assess an implemented branch against its TASK, approved contracts, and actual diff. **Not for** assessing the review report after the reviewer returns; use `/analyze` then.

| Mode | When to use | Example |
| --- | --- | --- |
| `INITIAL` | First independent review of a pushed task branch. | `/review initial TASK-02-025` |
| `RE-REVIEW` | Focused verification after corrections, using prior findings and correction commits. | `/review re-review TASK-02-025` |

**Default:** `INITIAL`. **Produces:** A copy-ready reviewer prompt. Review verdicts are advisory; acceptance remains human-owned.

### 6. Review findings analysis — `/analyze` / `ANALYZE`

**Skill:** [dev-code-review-analysis](skills/dev-code-review-analysis/SKILL.md)

**Use for:** Evaluating an independent review report: verify material findings against evidence, separate real defects from unsupported claims, propose dispositions, and group an efficient correction package. **Not for** independently reviewing an entire branch or generating the CORRECT prompt.

**Modes:** No formal named modes. Typical uses:

- `/analyze` — assess the review report already present in the conversation.
- `/analyze findings 1 and 3` — examine specific disputed findings.

**Produces:** Finding assessments (`CONFIRMED`, `PLAUSIBLE—NEEDS EVIDENCE`, `NOT SUBSTANTIATED`, `DESIGN/POLICY DECISION`), recommended dispositions, and decisions for human approval.

### 7. Agent follow-up — `/followup` / `FOLLOWUP`

**Skill:** [dev-agent-follow-up](skills/dev-agent-follow-up/SKILL.md)

**Use for:** A **short message back to an agent in the same conversation** after decisions or clarifications have already been made. Avoids copying TASK context, past findings, and approved contracts. **Not for** making the underlying decision or preparing a new-session handoff.

**Modes:** No formal named modes; it composes the **approved decision/instruction delta**.

- `/followup` — turn the decisions just approved here into a copy-ready message.
- `/followup keep EXPLORE` — clarify that the agent must remain in EXPLORE, if that is the approved instruction.

**Produces:** Usually a few sentences of actionable agent instructions. Never implies permission to move from EXPLORE to IMPLEMENT, or to push/merge, without explicit human authorization.

### 8. Engineering decision support — `/decide` / `DECIDE`

**Skill:** [dev-engineering-decision-support](skills/dev-engineering-decision-support/SKILL.md)

**Use for:** A **specific consequential blocker** raised during specification, EXPLORE, implementation, or review. Check approved contracts, test whether the question truly requires human approval, compare credible alternatives, and recommend a decision. **Not for** broad architectural redesign or a fresh implementation plan.

**Modes:** No formal named modes. Examples:

- `/decide` — analyze the agent's latest blocker from the conversation.
- `/decide should this retry reuse the existing claim policy?` — analyze one precise engineering trade-off.

**Produces:** Evidence, options, recommendation, and a precise human decision request. After approval, use `/followup` for the minimal reply to the agent.

## Which skill should I use?

| Situation | Use |
| --- | --- |
| Define, challenge, evolve, or reconcile **system-wide architecture** | `/arch` |
| Decide **which TASKs exist** and in what order | `/plan` |
| Specify **what one TASK must deliver** | `/spec` |
| Ask the coding agent to **explore, implement, or correct** | `/exec` |
| Ask an independent reviewer to **review a branch** | `/review` |
| Evaluate **findings returned by the reviewer** | `/analyze` |
| Resolve a **new material engineering question** | `/decide` |
| Send an **already-approved answer to an existing agent session** | `/followup` |

## End-to-end workflow and approvals

Requirements and constraints → `/arch design` → **human architecture approval** → `/plan create` → **human plan approval** → `/spec TASK-ID` → `/exec explore TASK-ID` → `/decide` if blocked → `/followup` for approved answers → **human implementation approval** → `/exec implement TASK-ID` → `/review initial TASK-ID` → `/analyze` if findings exist → **human correction decision** → `/exec correct TASK-ID` → `/review re-review TASK-ID` → **human acceptance**.

The workflow is illustrative, not a mandatory call to every skill for every task. Choose the **narrowest** relevant skill; avoid repeating already-completed analysis. Architecture owns system-level guarantees; planning owns task decomposition; specification owns one task contract; decision support owns narrow blockers; review analysis owns finding disposition; follow-up owns message composition only.

**Authorization is explicit.** A recommendation is not approval; a skill invocation is not permission to modify a repository, advance execution phases, push, merge, or mark a task DONE. Follow repository-specific instructions (including applicable `AGENTS.md`) and preserve independent review and mandatory verification.

## Repository and naming notes

The linked `dev-*` names above are the **current actual directory names and YAML skill identifiers**. The short names (`architecture`, `implementation-planning`, `task-specification`, `task-execution`, `code-review`, `review-analysis`, `agent-follow-up`, `decision-support`) are **proposed future rename targets**, not paths that already exist. Do not rewrite links or consumers to those names until a separate, approved rename migration is completed.

This repository is the maintained source of truth. Copies in other repositories can become outdated; update consumers deliberately and check internal/external references when renaming skills.
