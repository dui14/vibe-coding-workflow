---
name: bootstrap
description: Initialize or redesign the project's AI context, architecture rules, and development structure.
---

# Bootstrap

Use this skill only when initializing a new project or redesigning its AI development context.

## Goal

Create a minimal, consistent project context that allows coding agents to work without loading unnecessary information.

## Procedure

1. Inspect the repository structure.
2. Inspect package manifests, lockfiles, build configuration, and existing documentation.
3. Identify the actual runtime, frameworks, databases, external services, and development tools.
4. Identify architectural layers and their boundaries.
5. Create or update `ai-context/` using the project context structure.
6. Create or update the root `AGENTS.md`.
7. Add local `AGENTS.md` files only where a directory has distinct rules or boundaries.
8. Create required skills under `.agents/skills/`.
9. Remove duplicated, obsolete, or overly detailed rules from `AGENTS.md`.
10. Verify that documented architecture matches the actual codebase.

## Context

Use only the information required to define:

- Role and project purpose
- Product requirements
- Technology stack
- Architecture
- Database
- API contracts
- Coding standards
- UI system
- MCP/tools

## Rules

- Do not invent architecture or requirements.
- Prefer existing implementation over assumptions.
- Do not duplicate project knowledge between `AGENTS.md` and `ai-context/`.
- Keep `AGENTS.md` minimal.
- Do not modify application code unless required by the bootstrap task.
- Preserve working project behavior.