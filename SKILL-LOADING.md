# Skill Loading Contract — ChatGPT (Variant A)

When the user invokes a documented skill alias (for example `/exec explore TASK-02-025`) or explicitly requests a skill:

1. Fetch the current `skill-registry.yaml` from this repository's `main` branch. Do not resolve aliases from memory or README alone.
2. Match the requested alias or skill ID to **exactly one** registry entry; reject unknown or ambiguous names. Validate the requested named mode against that entry's `modes` list, if applicable.
3. Fetch the referenced `SKILL.md` from the **same Git commit** as the registry, and check that its YAML frontmatter `name` equals the registry ID. If a consistent snapshot cannot be fetched, report the limitation and stop rather than silently substituting remembered instructions.
4. Apply the loaded skill to the user's request, retaining all repository-specific instructions and human authorization gates. Reading a skill never authorizes repository changes.
5. If GitHub or the required file is unavailable, or validation fails, **fail closed**: state which skill could not be loaded and ask whether to retry. Never claim a skill was followed when it was not loaded.

This is a **behavioral contract for ChatGPT**, not an installed command dispatcher or a technical guarantee that a chat automatically reads this contract. It must be included in the ChatGPT project's/custom instructions (or supplied in the conversation) to govern invocation. Avoid copying complete SKILL.md content into those instructions; point to this registry and loading contract.

