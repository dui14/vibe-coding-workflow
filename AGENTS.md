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

---

## Context Loading

Read only the context required for the current task.

| Task | Context |
|---|---|
| Product / requirements | `ai-context/01-product.md` |
| Technology | `ai-context/02-tech-stack.md` |
| Architecture | `ai-context/03-architecture.md` |
| Database | `ai-context/04-database.md` |
| API / contracts | `ai-context/05-api-contract.md` |
| Coding | `ai-context/06-coding-standards.md` |
| UI | `ai-context/07-ui-system.md` |
| MCP / tools | `ai-context/08-mcp-tools.md` |

Read `ai-context/00-role.md` when task scope or agent role is unclear.

---

## Architecture Rules

Follow the layer boundaries defined in `ai-context/03-architecture.md`.

Local architecture rules override generic assumptions and are defined by the nearest `AGENTS.md`.

Do not bypass layer boundaries without an explicit requirement.

---

## Agent Invocation

Use the appropriate local `AGENTS.md` when modifying files inside a scoped directory.

Use project skills when the task matches an existing workflow.

For completed feature work, use the `finish-feature` workflow.

---

## Code Understanding with CodeGraph

CodeGraph indexed database is available at `.codegraph/codegraph.db`.Use this database to:
- Search for related code patterns and implementations
- Understand code structure and dependencies
- Find similar functions or classes
- Reference existing patterns when writing new code

When implementing features, first consult the codegraph database for similar implementations to maintain consistency and reuse patterns.

Use the CodeGraph MCP tool to:
1. Search for symbols: `searchNodes("UserService")`
2. Get callers/callees: `getCallers("getUserById")`
3. Trace impact radius: `getImpactRadius("src/db/schema.ts")`
4. Build context: `buildContext(nodeId)` → markdown summary

Results feed directly into your implementation context. 