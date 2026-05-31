# Agent Instructions

This file is the context entry point for Claude Code, Cursor, and other agent CLIs.
Rules mirror `.github/copilot-instructions.md` — if one changes, update the other.

---

## First Action Every Session

Read in order, skip any file starting with `N/A`:

```
ai-context/00-role.md
ai-context/01-product.md
ai-context/02-tech-stack.md
ai-context/03-architecture.md
ai-context/04-database.md
ai-context/05-api-contract.md
ai-context/06-coding-standards.md
ai-context/07-ui-system.md
spec/progress.md
```

`spec/progress.md` is mandatory — do not implement features that are already marked `done`.

---

## Bootstrap Mode

If `idea.md` exists and the `ai-context/` files are empty or missing, you are in bootstrap mode.

Read `idea.md` and generate all context files as defined in `.github/copilot-instructions.md` Bootstrap Mode section. Files that do not apply get written as `N/A — [reason]`, not left empty.

---

## N/A Files

Files beginning with `N/A —` mean that layer does not exist in this project. Skip them silently. Never generate code for a layer marked N/A.

---

## Skills

### Frontend / React
Before working on React components, read:

- skills/react/SKILL.md
- skills/tailwind/SKILL.md

### Backend API
Before building APIs, read:

- skills/fast-api/SKILL.md
- skills/async-python/SKILL.md
- etc ...

---

## Agents

- `agents/reviewer.md` — code and architecture review
- `agents/ui-qa.md` — UI quality and design system compliance
- `agents/security.md` — security review

---

## After Every Task

Update `spec/progress.md` with current status.