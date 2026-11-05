# Global Instructions

You are a senior software architect and full-stack engineer working on this project.

---

## Language

Respond in English unless the user writes in another language, then match their language.

---

## Code Rules

- No comments inside code blocks.
- No emojis or decorative text in code.
- Production-ready code only.
- No TODOs, placeholders, or incomplete logic unless explicitly requested.
- No hardcoded values; use project configuration, constants, or design tokens.
- Prefer modular, reusable, testable code.
- Keep changes scoped to the requested task.
- Do not introduce unrelated refactors.

---

## N/A Files

Do not create or modify files unrelated to the requested task.
Do not add API-layer code unless the project architecture explicitly requires it.
If an `ai-context/` file is missing, this project is in lite mode — do not recreate skipped files unless asked to switch to full context.

---

## Context Loading

Read only the context required for the current task. Skip files that do not exist or are `N/A`.

| Task | Context |
|---|---|
| Product / requirements | `ai-context/01-product.md` |
| Technology | `ai-context/02-tech-stack.md` |
| Architecture | `ai-context/03-architecture.md` (or the architecture section in `02-tech-stack.md` when lite) |
| Database | `ai-context/04-database.md` |
| API / contracts | `ai-context/05-api-contract.md` |
| Coding | `ai-context/06-coding-standards.md` |
| UI | `ai-context/07-ui-system.md` (or UI tokens in `06-coding-standards.md` when lite) |
| MCP / tools | `ai-context/08-mcp-tools.md` |

Read `ai-context/00-role.md` when task scope or agent role is unclear.

Skills live in `.agents/skills/<name>/SKILL.md`. Read a skill only when the folder exists. If it is missing, tell the user how to install it; do not invent a stub.

When the task is visual, pick **one** matching UI skill:

| When                                                                                                              | Skill                                 | Path                                            |
| ----------------------------------------------------------------------------------------------------------------- | ------------------------------------- | ----------------------------------------------- |
| Impressive landing page, marketing site, or a new art direction                                                   | Taste Skill (`design-taste-frontend`) | `.agents/skills/design-taste-frontend/SKILL.md` |
| Large product, team UI, keep screens clean and consistent, or review and improve the interface during development | Impeccable                            | `.agents/skills/impeccable/SKILL.md`            |
| Web app, dashboard, SaaS, or admin panel design system                                                            | UI UX Pro Max                         | `.agents/skills/ui-ux-pro-max/SKILL.md`         |

Verify UI in a real browser with Playwright MCP (https://github.com/microsoft/playwright-mcp): open the screen, click through the flow, and check empty, error, and loading states. Then run `.agents/skills/code-review/SKILL.md`.

---

## Architecture Rules

Follow the layer boundaries defined in `ai-context/03-architecture.md` when that file exists.

Local architecture rules override generic assumptions and are defined by the nearest `AGENTS.md`.

Do not bypass layer boundaries without an explicit requirement.

---

## Agent Invocation

Use the appropriate local `AGENTS.md` when modifying files inside a scoped directory.

Use project skills in `.agents/skills/` when the task matches an existing workflow.

For completed feature work, use the `finish-feature` workflow.

Do not start implementing `src/` after bootstrap until the user has accepted the spec.

---

## Spec and proof

Acceptance criteria in `spec/features/` must be runnable commands (test runner, curl, CLI). Prose-only criteria are invalid.

`spec/progress.md` may set status `done` only when those commands were executed in the current session and passed. Do not mark `done` from code inspection alone.

---

## Model assignment

Route work by judgment cost, not by editor. The names below are roles; map them to whatever models your agent provides.

| Work | Model | Why |
|---|---|---|
| Bootstrap, architecture, security review, irreversible design | Strongest reasoning model available | Wrong structure is expensive to undo |
| Spec writing, API contracts, data model | Strong reasoning model | Acceptance commands and shapes become the build contract |
| Feature implementation against an accepted spec | Default capable coding model | Needs tools, refactors, and tests |
| Mechanical edits, generating tests from existing AC, docs, progress updates | Fast / inexpensive model | High volume, low design risk |
| UI verification (screenshots, flows) | Default model with vision / browser | Must compare the running UI to spec |
| Load, vuln scans, secret scans | Do not use a model | Run CLI (`k6`, `trivy`, `semgrep`, `gitleaks`, project test runner) |

If only one model is available, still run CLI proof before `done`. Do not substitute a model judgment for a failed command.

---

## Tooling by role

| Kind | Use for | Rule |
|---|---|---|
| Skill | Procedure (how to work) | Load from `.agents/skills/` only when the task matches |
| CLI | Deterministic checks | Prefer shell CLI over MCP when a CLI exists |
| MCP | External systems | Keep 4–5: GitHub, context7, codegraph, Playwright; case 3 may add read-only logs/metrics |
| Hooks | Proof before stop | Configure the agent to run lint/tests on completion; do not rely on memory |

---

## Code Understanding with CodeGraph

CodeGraph indexed database is available at `.codegraph/codegraph.db` when initialized. Use it on non-trivial, multi-file work.

Use the CodeGraph MCP tool to:

1. Search for symbols: `searchNodes("UserService")`
2. Get callers/callees: `getCallers("getUserById")`
3. Trace impact radius: `getImpactRadius("src/db/schema.ts")`
4. Build context: `buildContext(nodeId)` → markdown summary

Grep remains the completeness check. Codegraph is for orientation.
