# MCP Tools

Document only the servers this project actually enables (keep 4–5). Agents already have workspace file tools — do not add a filesystem MCP.

Prefer a local CLI when one exists (`gitleaks`, `semgrep`, `trivy`, `k6`, the project test runner). MCP descriptions are loaded every turn; CLI is not.

Config file depends on the agent (examples: `.mcp.json`, `.cursor/mcp.json`, `.vscode/mcp.json`). Use the same server list in whichever file your agent reads.

**Tool-first rule**: before writing library-specific code, fetch live docs (context7). Before marking UI done, drive the running app (Playwright or browser). Before claiming `progress.md` done, run the acceptance commands in the shell.

---

## context7

**What it does**: Fetches current, version-accurate documentation for a library from the official source.

**Use it when**:
- Implementing anything in `ai-context/02-tech-stack.md`
- Version-sensitive APIs, hooks, or config
- Type errors that suggest a mismatch with the installed version

**Never use training memory for**: framework APIs, ORM schema syntax, CSS utility names, component props. Fetch from context7 first.

---

## github

**What it does**: Read and write GitHub repositories: issues, pull requests, search, file contents.

**Use it when**:
- Turning review findings into issues
- Opening a PR after a feature whose acceptance commands passed
- Searching public examples
- Reading a dependency changelog

**Environment**: `GITHUB_TOKEN` or the agent's GitHub OAuth. Do not commit secrets.

---

## playwright

**What it does**: Browser automation — navigate, click, type, screenshots, DOM inspect against localhost.

**Use it when**:
- After a UI section, compare the running screen to spec
- Responsive checks at documented breakpoints
- User-flow proof before `finish-feature`

Use Playwright MCP (https://github.com/microsoft/playwright-mcp) as the UI gate: click through the real flow, then run `code-review`.

**Note**: the dev server must be running first.

---

## codegraph

**What it does**: Semantic navigation (symbols, callers, impact) on an indexed tree-sitter graph.

**Use it when**:
- Multi-file orientation (Case 2 especially)
- Finding existing patterns before adding a feature
- Estimating blast radius of a change

Grep is the completeness check. Codegraph is for orientation. Skip it on single-file edits.

Install: https://github.com/colbymchenry/codegraph

---

## Case 3 only — read-only logs/metrics

Add at most one extra server for production logs or metrics, **read-only**. Do not give the default agent write access to prod. Prefer vendor CLIs when they exist.

---

## Do not add by default

filesystem, chrome-devtools, markitdown, sequential-thinking, and similar. If you add one, remove another so the enabled set stays at 4–5.

---

## Adding a server

1. Add it to the MCP config your agent loads
2. Document it here: what, when, how
3. State which existing server it replaces if the count would exceed 5
