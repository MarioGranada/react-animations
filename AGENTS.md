# AGENTS.md — React Animations — Challenges

Compact guide for future OpenCode sessions. It records only the facts an agent is likely to miss or get wrong.

## Quickstart

| Command | Description |
| --- | --- |
| `npm install` | Install dependencies. |
| `npm run dev` | Start Vite at http://localhost:5173. |
| `npm run build` | Verify the production bundle. |
| `npm run lint` | Run ESLint. |

## Requirements

- Node.js 18+.
- npm (a `package-lock.json` is committed).
- A modern browser; animations are tested in Chromium-based browsers.

## Environment

- No environment variables are used.
- The modal portal requires the `#modal` element in `index.html`.

## Architecture

- `src/App.jsx` — router configuration.
- `src/pages/Welcome.jsx` — scroll-linked hero animations.
- `src/pages/Challenges.jsx` — page shell and context provider.
- `src/store/challenges-context.jsx` — challenge data and actions.
- `src/components/` — tabs, list, item, modal, and form.

## Commands and build order

- Use `npm run dev` for animation work; production builds can hide timing issues.
- `npm run lint` and `npm run build` are the gates; there are no tests.

## Conventions and gotchas

- AnimatePresence only animates exit when its direct children are motion components with stable keys.
- Do not put a provider inside a component that unmounts on route change if state must survive navigation.
- The `layoutId` indicator only works while both tabs render inside the same layout tree.
- Portal content is outside the React root’s DOM subtree; global CSS must still target it.
- Respect `prefers-reduced-motion` before adding more scroll effects.

## Memory

- Read `MEMORY.md` first to understand the current status and decisions.
- Before changing behaviour, read `constitution.md` and keep the change aligned with it.
- After a task, update `MEMORY.md` with status, decisions, and mistakes to avoid. Keep it short.
- If a rule becomes permanent, move it into this file instead of leaving it in memory.
- Never store secrets, tokens, or personal data in `MEMORY.md`.
