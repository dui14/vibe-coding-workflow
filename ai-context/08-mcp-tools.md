# MCP Tools

This file documents the MCP servers configured in `.vscode/mcp.json`.
Copilot reads this file to know what tools are available and when to use them instead of generating code from memory.

**Tool-first rule**: before writing implementation code, check if an MCP tool can do the task better. MCP tools have access to live data — Copilot's training data does not.

---

## context7

**What it does**: Fetches current, version-accurate documentation for any library directly from the official source.

**Use it when**:
- Implementing anything that uses a library defined in `ai-context/02-tech-stack.md`
- The library version matters (API shapes change between versions)
- Unsure about a specific method signature, hook behavior, or configuration option
- Seeing type errors that suggest the code doesn't match the installed version

**How to invoke**:
```
Use context7 to fetch the current documentation for [library name] [version].
Then implement [feature] using the correct API.
```

**Never use Copilot's memory for**: React hook APIs, Next.js router behavior, Prisma schema syntax, Tailwind class names, shadcn/ui component props. Always fetch from context7 first.

---

## github

**What it does**: Read and write to GitHub repositories. Create issues, open pull requests, search code, read file contents from any public or permissioned repo.

**Use it when**:
- Converting agent review findings into GitHub issues
- Opening a PR after completing a feature
- Searching for real-world implementation examples in public repos
- Reading the CHANGELOG of a dependency to understand breaking changes

**How to invoke**:
```
Use the github MCP tool to create an issue in this repo titled "[title]" with the following body: [body].
```

```
Use the github MCP tool to search for examples of [pattern] in public Next.js repos.
```

**Environment**: requires `GITHUB_TOKEN` set in your shell environment or `.env.local` (not committed).

**Authentication**:
Supports both OAuth and Personal Access Token (PAT).
- Recommended:
Use OAuth with the remote GitHub MCP server:
https://api.githubcopilot.com/mcp/

- OAuth removes the need to manually manage GITHUB_TOKEN or PAT secrets.

---

## playwright

**What it does**: Full browser automation — navigate, click, type, take screenshots, inspect the DOM. Can run against localhost during development.

**Use it when**:
- After implementing a UI section, take a screenshot to verify it visually
- Testing responsive layout at specific viewport widths (375px mobile, 768px tablet, 1440px desktop)
- Running a user flow end-to-end before the feature is marked done
- The `ui-qa` agent needs to verify something it can't determine from code alone

**How to invoke**:
```
Use playwright to open http://localhost:3000/[path] and take a screenshot at viewport width 375px.
Compare the screenshot against the spec in spec/ui/[screen-name].md and report differences.
```

```
Use playwright to run this user flow: [describe steps]. Report any errors or unexpected behavior.
```

**Note**: the dev server must be running (`npm run dev` or equivalent) before invoking playwright.

---

## filesystem

**What it does**: Direct read/write access to the workspace folder. Faster than reading files one by one through Copilot's normal context.

**Use it when**:
- Reading all files in `ai-context/` at the start of a session
- Writing multiple generated spec files to disk at once (during bootstrap)
- Scanning `src/` to understand the current state of the codebase before implementing

**How to invoke**:
```
Use the filesystem tool to read all .md files in ai-context/ and return their contents.
```

```
Use the filesystem tool to list all files in src/ recursively.
```

---


---

## chrome-devtools-mcp

**What it does**: Connects the assistant to Chrome DevTools so it can inspect the live browser, DOM, console, network requests, and runtime state.

**Use it when**:
- Debugging frontend bugs that are easier to verify in a real browser
- Checking console errors, failed requests, or hydration issues
- Inspecting rendered DOM, styles, or event behavior
- Verifying an interaction after a UI change

**How to invoke**:
```
Use chrome-devtools-mcp to open the current page, inspect the DOM, and check console/network activity for errors.
```

---

## markitdown-mcp

**What it does**: Converts documents into Markdown so the assistant can read and summarize content from files like PDFs, Word docs, and other supported formats.

**Use it when**:
- You need to extract readable text from a document
- Summarizing long files before editing or analysis
- Converting source material into Markdown for further processing
- Working with uploaded files that are not plain text

**How to invoke**:
```
Use markitdown-mcp to convert [file] into Markdown, then summarize or extract the sections I need.
```

**Server commands**:
```bash
# STDIO (default)
markitdown-mcp

# Streamable HTTP / SSE
markitdown-mcp --http --host 127.0.0.1 --port 3001
```

---

## notebooklm mcp

**What it does**: Bridges the assistant with NotebookLM-style research notebooks so it can work across stored sources, notes, and summaries in one place.

**Use it when**:
- You are collecting and comparing research notes
- Summarizing source material inside a notebook workflow
- Extracting key ideas, quotes, or action items from notebook content
- Organizing knowledge around a project or topic

**How to invoke**:
```
Use notebooklm mcp to search the notebook sources, summarize the selected notes, and extract the key points.
```

---

## Sequential Thinking MCP

**What it does**: Helps the assistant solve complex problems by breaking them into ordered steps, tracking assumptions, and revising the plan as new information appears.

**Use it when**:
- A task has multiple dependent steps
- You need careful debugging or root-cause analysis
- Comparing approaches before choosing one
- Planning architecture, implementation, or migration work

**How to invoke**:
```
Use Sequential Thinking MCP to break this problem into steps, track assumptions, and update the plan after each step.
```

---

## supabase mcp

**What it does**: Gives the assistant direct access to Supabase project resources such as database schema, SQL, auth, storage, and related project settings.

**Use it when**:
- Inspecting or updating database tables and relationships
- Debugging auth, RLS, or storage configuration
- Running SQL against a Supabase project
- Verifying project-side settings before shipping a feature

**How to invoke**:
```
Use supabase mcp to inspect the schema, run the SQL I provide, and verify the auth/storage configuration for this project.
```

**Optional bonus**: create a dedicated workspace for each Supabase-backed app so SQL, migrations, and environment context stay isolated and easier to manage.

## Adding More Servers

To add a new MCP server:

1. Add the server config to `.vscode/mcp.json` following the existing pattern
2. Add a section to this file documenting: what it does, when to use it, how to invoke it
3. Update the relevant section in `.github/copilot-instructions.md` if the server applies to a specific task type

Popular servers for web development: `@supabase/mcp`, `@vercel/mcp`, `sentry/mcp`, `firecrawl` (web scraping), `browser-use` (autonomous browsing). Find more at skills.sh.