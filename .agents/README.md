# Skills

This folder holds agent skills. Project skills that ship with this repo live under `.agents/skills/<name>/SKILL.md`. Extra skills from [skills.sh](https://www.skills.sh) also install here.

Skills are reusable procedures. The agent reads the matching `SKILL.md` before a task. You do not need to paste the procedure into every prompt.

If a skill folder is missing, follow the install command in this file. Do not invent a stub folder.

---

## Skills that ship in this repo

| Task | Skill path |
|---|---|
| New project context and spec | `.agents/skills/bootstrap/SKILL.md` |
| Finished a feature | `.agents/skills/finish-feature/SKILL.md` |
| Bug fix | `.agents/skills/fix-bug/SKILL.md` |
| Review implementation | `.agents/skills/code-review/SKILL.md` |
| Navigate a large repo | `.agents/skills/codegraph/SKILL.md` |
| Security review (use if the skill file has content) | `.agents/skills/security/SKILL.md` |
| Landing page or new art direction | `.agents/skills/design-taste-frontend/SKILL.md` |
| Review and improve UI on a larger product | `.agents/skills/impeccable/SKILL.md` |

---

## Building UI

Pick **one** skill for the surface you are building. Read that `SKILL.md` only if the folder exists.

| When to use | Skill | Path |
|---|---|---|
| Impressive landing page, marketing site, or a clear new art direction | Taste Skill (`design-taste-frontend`) | `.agents/skills/design-taste-frontend/SKILL.md` |
| Large project, team work, screens that must stay clean, consistent, and professional; also for direction, review, and polish during development | Impeccable | `.agents/skills/impeccable/SKILL.md` |
| Web app, dashboard, SaaS, or admin panel — design system and UI/UX patterns | UI UX Pro Max | `.agents/skills/ui-ux-pro-max/SKILL.md` (not shipped; install first) |

Taste Skill and Impeccable are already in this repo. UI UX Pro Max is optional:

```bash
npx skills add https://github.com/nextlevelbuilder/ui-ux-pro-max-skill --skill ui-ux-pro-max
```

If you need to reinstall Taste Skill or Impeccable:

```bash
npx skills add https://github.com/Leonxlnx/taste-skill --skill "design-taste-frontend"
npx skills add pbakaus/impeccable
```

---

## UI quality assurance

Recommended method: your coding agent plus Microsoft Playwright MCP.

https://github.com/microsoft/playwright-mcp

Start the app. Ask the agent to open the screen, click through the real user flow, and check empty, error, and loading states. Compare the running UI to `spec/ui/` or `spec/features/`. A single screenshot is not enough. Then run `.agents/skills/code-review/SKILL.md`.

Claude Code:

```bash
claude mcp add playwright npx @playwright/mcp@latest
```

Other agents: copy the `playwright` server from `.vscode/mcp.json` into the MCP config your agent loads.

---

## Optional skills (install only when you need them)

```bash
npx skills add owner/repo-name
```

That downloads files into `.agents/skills/`.

### Web / full-stack extras

```bash
npx skills add vercel-labs/agent-skills
npx skills add shadcn/ui
npx skills add vercel-labs/next-skills
npx skills add better-auth/skills
npx skills add supabase/agent-skills
```

### Anthropic public skill set

Examples, document workflows, and a skill-creator. Install only if you need those:

https://github.com/anthropics/skills/

```bash
npx skills add anthropics/skills
```

### Case 2 and case 3 

Add these procedures when you leave greenfield work:

| Task | Skill to add |
|---|---|
| Learn existing code | `onboard-codebase` |
| Lock current behavior in tests | `characterize-tests` |
| Finish missing pieces | `gap-fill` |
| Incoming defects | `triage-bug` |
| Load and growth | `perf-scale` |
| Deploy and operations readiness | `devops-readiness` |

Skills describe how to work. Command-line tools prove results. MCP talks to outside systems (keep four or five servers). Do not replace Playwright MCP or the test runner with extra skills.

Browse more at: https://www.skills.sh

---

## Tooling reminder

Prefer command-line tools (`gitleaks`, `semgrep`, `trivy`, `k6`, the project test runner) over new MCP servers. Configure a completion hook so tests and lint run before the agent stops.
