# React Animations — Challenges

A challenge tracker used to practise animation in React with Framer Motion. The welcome page reacts to scroll position, the challenge list animates between tabs and states, and the new-challenge modal validates input with an animated shake.

Challenges live in memory for the session: they can be created, marked completed or failed, expanded, and deleted. The project is about animation technique, not persistence.

> **Follow-along project.** This app was built while following **React — The Complete Guide (Academind / Maximilian Schwarzmüller)**. It is included in the portfolio as a learning exercise, not as a production product. The implementation is my own work based on the course material.

## Live demo

| | |
| --- | --- |
| **Live site** | https://mariogranada.github.io/react-animations/ |
| **Repository** | https://github.com/MarioGranada/react-animations |
| **Portfolio summary** | Framer Motion playground: a challenge tracker with scroll-linked parallax, shared-layout tabs, animated list transitions and a shake-validated modal form. |

## Features

- Scroll-linked parallax and opacity on the welcome page.
- Animated route-level pages with React Router.
- Tab indicator that moves with a shared `layoutId`.
- Animated list entry, exit, and reordering with `AnimatePresence`.
- Expandable challenge details with height animation.
- Modal entrance/exit animation through a portal.
- Staggered image picker and shake validation using `useAnimate`.
- Challenge context for add, delete, and status changes.

## Tech stack

| Layer | Technology |
| --- | --- |
| Framework | React 18 + Vite |
| Animation | Framer Motion 11 |
| Routing | React Router 6 |
| State | React Context |
| Styling | Plain CSS |

## Project structure

```text
react-animations/
├── src/
│   ├── pages/
│   │   ├── Welcome.jsx        # Scroll-linked hero
│   │   └── Challenges.jsx     # Challenges page + provider
│   ├── components/
│   │   ├── Header.jsx         # Add Challenge button + modal presence
│   │   ├── Challenges.jsx     # Tabs, filtered list, presence
│   │   ├── ChallengeTabs.jsx  # Shared layout indicator
│   │   ├── ChallengeItem.jsx  # Status actions and expandable details
│   │   ├── NewChallenge.jsx   # Form, image picker, shake validation
│   │   ├── Modal.jsx          # Portal dialog
│   │   └── Badge.jsx
│   ├── store/challenges-context.jsx
│   ├── assets/                # Images and image metadata
│   ├── App.jsx
│   └── main.jsx
└── index.html
```

## Getting started

### Requirements

- Node.js 18+.
- npm (a `package-lock.json` is committed).
- A modern browser; animations are tested in Chromium-based browsers.

### 1. Install dependencies

```bash
npm install
```

### 2. Run locally

**Start the development server**

```bash
npm run dev
```

Open http://localhost:5173.

The app has two routes: `/` and `/challenges`.

### Available scripts

| Command | Description |
| --- | --- |
| `npm run dev` | Start Vite on port 5173. |
| `npm run build` | Build the app into `dist/`. |
| `npm run preview` | Preview the production build. |
| `npm run lint` | Run ESLint over JS/JSX files. |

## How it works

`App.jsx` creates a browser router with `WelcomePage` at `/` and `ChallengesPage` at `/challenges`.

`WelcomePage` uses `useScroll` and `useTransform` to move and fade the city, hero, and heading as the page scrolls. No animation state is stored in React.

`ChallengesPage` wraps the header and main content in `ChallengesContextProvider`, so the add form, tabs, and list share one challenge array.

`Challenges` filters challenges into active, completed, and failed, then renders the selected tab inside `AnimatePresence`. `ChallengeTabs` uses a shared `layoutId` so the indicator slides between tabs.

`NewChallenge` validates with refs; invalid input triggers a staggered shake via `useAnimate` instead of a browser alert. `Modal` renders into `#modal` with `createPortal` and animates its dialog.

`ChallengeItem` changes status through context and expands details with an `AnimatePresence` height animation.

## Deployment

- **Live:** `.github/workflows/deploy.yml` builds the app on every push to the default branch and publishes `dist/` (plus a `404.html` SPA fallback) to the `gh-pages` branch, which GitHub Pages serves at https://mariogranada.github.io/react-animations/.
- Target: GitHub Actions can build the Vite app and publish `dist/` to GitHub Pages.
- Because the app uses client-side routing, the host must rewrite unknown paths to `index.html`; otherwise a direct visit to `/challenges` returns 404.
- Set the Vite `base` option to the repository path when deploying to a project Pages site.
- No backend or database is required.

## Notes and limitations

- Challenges are in memory only and reset on reload.
- `#modal` must exist in `index.html`; the portal has no fallback container.
- The welcome page has no reduced-motion handling; scroll animations run for every user.
- The `Badge` component is keyed by caption to replay its animation when counts change.
- There are no tests.

---

**Author:** Mario Granada
