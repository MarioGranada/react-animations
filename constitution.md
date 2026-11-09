# Project Constitution — React Animations — Challenges

This document defines the non-negotiable foundations for this repository. Read it before adding or changing features.

## Guiding Principles

- **Simplicity first** — prefer the smallest solution that solves the problem. If a change needs a long explanation, it is probably over-engineered.
- **No hardcoded secrets or endpoints** — configuration belongs in environment variables; visual design tokens belong in styles, not in `.env` files.
- **Traceability** — every value, dependency, and route should make its origin and purpose obvious.
- **Debuggability** — fail loudly and visibly; avoid silent fallbacks that hide broken data.
- **Official patterns** — use the documented API of each framework and library before inventing a workaround.
- **Portfolio clarity** — this repository is part of a public portfolio. Code should read as clean, intentional, and easy for a reviewer to follow. As a follow-along project, its purpose is to demonstrate the concepts practised in the course, not to imitate production scale.

## Technology Stack Foundations

| Layer | Choice | Rationale |
| --- | --- | --- |
| Framework | React 18 + Vite | Fast iteration for animation experiments. |
| Animation | Framer Motion 11 | Declarative motion, layout animations, and presence handling. |
| Routing | React Router 6 | Two routes: welcome and challenges. |
| State | React Context | Challenge data is shared by the header, tabs, list, and modal. |
| Styling | Plain CSS | Keeps animation behaviour separate from a UI library. |

**Rule of thumb:** a new dependency must solve a concrete problem that the current stack cannot solve cleanly. Justify it in the change that introduces it.

## Core Premises

### 1. Scope

An animation-focused course project. The goal is to demonstrate Framer Motion patterns cleanly, not to build a persistent challenge product. Backend, accounts, and data durability are out of scope.

### 2. Environment Isolation

- This project has no runtime secrets. Do not introduce `.env` files unless a real secret or environment-specific URL appears.
- If configuration is added, use environment variables and document them in the README.
- Never commit keys, tokens, database URLs, or credentials.

### 3. Architecture

- Page-level routing lives in `App.jsx`; animation details stay inside the component that owns the element.
- Shared challenge state belongs in `store/challenges-context.jsx`.
- Reusable motion patterns should be extracted only after they appear in more than one component.

### 4. Data and State

- Challenges are client-only state and reset on reload.
- Status changes are synchronous; there is no server or optimistic request.
- Keep derived lists (`active`, `completed`, `failed`) computed from the single challenge array.

### 5. Styling and UX

- Global styles live in `src/index.css`; component class names are shared across the page.
- Animation timing should be consistent: short springs for interaction, longer easing for page transitions.
- Keep the modal readable and focusable; animation must not block interaction.

### 6. Quality Gates

- `npm run lint` and `npm run build` are the gates.
- Manually test adding a challenge, invalid submission, tab switching, status changes, expanding details, deleting, and direct navigation to `/challenges`.
- Check animations in a production build and with reduced motion enabled.

### 7. Deployment

- Build with Vite and publish `dist/` through GitHub Actions.
- Configure SPA fallback and the correct base path for GitHub Pages.
- No server runtime is required.

## What to Avoid

- Animating layout properties that trigger expensive reflows when a transform would work.
- Storing derived challenge lists in state.
- Removing `AnimatePresence` wrappers without checking exit animations.
- Assuming the portal container exists.
- Adding a backend for a demo whose purpose is animation.

## Checklist Before Adding Anything New

- Does this solve a real problem for this project, or am I adding scope for its own sake?
- Is every new value configuration-driven rather than hardcoded?
- Does the change follow the existing folder and naming patterns?
- Is there a clear failure path when data, the network, or the environment is unavailable?
- Have I run the available lint/build/test command and fixed what it reports?
- Did I update `README.md` and `MEMORY.md` if behaviour or setup changed?

## Philosophy Statement

This repository exists to show thoughtful front-end engineering: clear structure, readable code, and deliberate trade-offs. The goal is not to use every tool available, but to make every file explain itself. Simplicity is the feature.
