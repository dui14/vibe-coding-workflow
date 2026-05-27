# Skills

This folder contains agent skills installed from [skills.sh](https://www.skills.sh).

Skills are reusable procedural knowledge files. Copilot reads the relevant skill before a task to get expert-level guidance for that specific domain — without you having to explain it in every prompt.

---

## Installing Skills

```bash
npx skills add owner/repo-name
```

This downloads the skill files into this `skills/` folder.

### Recommended for web / full-stack projects

```bash
# UI and design
npx skills add vercel-labs/agent-skills          # React, composition patterns, Vercel deploy
npx skills add shadcn/ui                          # shadcn/ui component usage
npx skills add leonxlnx/taste-skill              # High-end visual design taste

# Next.js
npx skills add vercel-labs/next-skills           # Next.js best practices

# Auth
npx skills add better-auth/skills               # better-auth patterns

# Database
npx skills add supabase/agent-skills            # Supabase + Postgres
```

### Recommended for personal sites / landing pages

```bash
npx skills add vercel-labs/agent-skills         # Deployment + React patterns
npx skills add leonxlnx/taste-skill            # Design taste for minimal/editorial UI
npx skills add pbakaus/impeccable              # Polish, audit, animate
```

### Other useful skills

```bash
npx skills add mattpocock/skills               # TDD, debugging, architecture improvement
npx skills add obra/superpowers               # Systematic debugging, code review
```

Browse more at: https://www.skills.sh

---

## How Copilot Uses Skills

`copilot-instructions.md` tells Copilot which skill to read before each task type:

| Task | Skill loaded |
|---|---|
| Building UI components | `skills/frontend-design` or `skills/ui-ux-pro-max` |
| Using shadcn/ui | `skills/shadcn` |
| Setting up auth | `skills/better-auth-best-practices` |
| Supabase / Postgres | `skills/supabase-postgres-best-practices` |
| Deploying to Vercel | `skills/deploy-to-vercel` |
| Debugging | `skills/diagnose` or `skills/systematic-debugging` |
| Polishing UI | `skills/polish` or `skills/impeccable` |

Copilot checks `skills/` for the relevant file before starting. If the file doesn't exist, it proceeds without it. You never need to reference skills manually in your prompts.

---

## Adding Your Own Skills

Create a `.md` file in this folder with any procedural knowledge you want Copilot to apply consistently — company code standards, a specific design system, a recurring pattern you use across projects.

Then register it in `copilot-instructions.md` under the Skills section with the task type it applies to.