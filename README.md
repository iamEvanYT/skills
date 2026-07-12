# Evan's Personal Skills

Reusable agent skills built from practical workflows and domain expertise.

## Install

Install skills directly from GitHub:

```bash
npx skills@latest add iamEvanYT/skills
```

Or with Bun:

```bash
bunx skills@latest add iamEvanYT/skills
```

To install one skill, select it when prompted or pass its name to the installer.

## Skills

- [write-system-prompts](./skills/write-system-prompts/SKILL.md) — Design, review, debug, and evaluate robust system prompts and agent instruction policies.

## Structure

Each skill lives in `skills/<skill-name>/` and follows the Agent Skills format:

```text
skills/<skill-name>/
├── SKILL.md
├── agents/openai.yaml    # Optional Codex interface metadata
├── references/          # Detailed guidance loaded only when needed
├── scripts/             # Optional executable helpers
└── assets/              # Optional output resources
```

Keep `SKILL.md` focused on the core workflow. Put detailed material in `references/` and add scripts or assets only when the skill actually uses them.
