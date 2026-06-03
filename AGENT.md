# Agent Instructions

This file is the context entry point for Antigravity, Cursor, and other agent CLIs.
> Rules mirror `.github/copilot-instructions.md` — if one changes, update the other.
> If you want to add another section here (Recommended) update the same section in [.github/copilot-instructions.md](.github/copilot-instructions.md) as well.
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

### My Custom Domain
Before working on feature X, read:

- skills/my-custom/SKILL.md

---

## Code Understanding with CodeGraph

Before implementing a feature, you can search the codebase for:
- Function signatures and implementations
- Import/export relationships
- API endpoints and route handlers
- Component definitions and usage
- Type definitions and interfaces

Use the CodeGraph MCP tool to:
1. Search for symbols: `searchNodes("UserService")`
2. Get callers/callees: `getCallers("getUserById")`
3. Trace impact radius: `getImpactRadius("src/db/schema.ts")`
4. Build context: `buildContext(nodeId)` → markdown summary

Results feed directly into your implementation context. 