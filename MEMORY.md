# React Animations — Challenges — Working Memory

_Last updated: 2026-11-02_

## Current status

- Welcome and challenges routes are implemented.
- Create, status change, expand, delete, tab filtering, and validation shake work.
- Animations use Framer Motion presence, layout, scroll, and imperative APIs.
- No tests or deployment workflow yet.

## Key decisions

- Used context instead of prop drilling because the header, tabs, list, and modal all touch challenge data.
- Used a portal for the modal so it escapes the page stacking context.

## Known limitations and follow-ups

- Challenges are not persisted.
- No reduced-motion support.
- No tests for animation behaviour.
- No deployment configuration or SPA fallback documented in code.

## Mistakes to avoid

- Forgetting the `#modal` element breaks the new-challenge modal.
- A missing key on a list item prevents exit animations.
- Directly opening `/challenges` on a static host without a rewrite returns 404.

## Next steps

- Add `prefers-reduced-motion` handling.
- Persist challenges in `localStorage` or a backend.
- Add a GitHub Pages workflow with SPA fallback.

---

Keep this file under ~60 lines. Summarise or delete notes that no longer add value.
