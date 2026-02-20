# STACK

## Runtime
- Node: 22.x
- Package Manager: npm (or pnpm)

## Backend
- Framework: Nitro (Nuxt built-in server engine) / Node.js
- Data Persistence: Nuxt Content (Markdown-based) or SQLite with Prisma
- Key directories: `/server`, `/content`

## Frontend
- Framework: Nuxt 4 (Latest)
- CSS: Tailwind CSS
- Component Library: Nuxt UI (optional, recommended)
- Key directories: `/components`, `/pages`, `/layouts`, `/assets`

## Validation Commands
- Lint: `npm run lint`
- Test: `npm run test`
- Build: `npm run build`
- Dev: `npm run dev`

## Branch and Commit Policy
- Default branch: main
- Task branch pattern: codex/<task-id>-<slug>
- Commit message pattern: <task-id>: <summary>

## Task Status Policy
- codex_dev_done: Issue status moved to 'Agent work DONE'
- codex_test_done: Issue status moved to 'In Review'
- codex_review_ready: Pull Request created and linked

## Issue Tracker Policy
- Linear state mapping: `/agents/_shared/LINEAR_WORKFLOW.md`
- Required completion comment format: `AGENT_EVENT_V1` as per `/agents/_shared/LINEAR_COMMENT_SCHEMA.md`
