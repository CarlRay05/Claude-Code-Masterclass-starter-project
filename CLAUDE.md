# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm run dev       # Start dev server at http://localhost:3000
npm run build     # Production build
npm run lint      # ESLint
npm run test      # Run all tests (Vitest, watch mode)
npx vitest run    # Run tests once (CI mode)
npx vitest run tests/components/Navbar.test.tsx  # Run a single test file
```

## Architecture

**Next.js App Router** with two route groups:

- `app/(public)/` — Unauthenticated pages (splash, login, signup, preview). Layout wraps content in `.public` and `.center-content` CSS classes.
- `app/(dashboard)/` — Authenticated pages under `/heists`. Layout includes the `Navbar` component. Pages use `.page-content` for consistent centering/width.

**Components** live in `components/<ComponentName>/` with an `index.ts` barrel export. CSS Modules (`.module.css`) are used for component-scoped styles alongside Tailwind utilities.

**Tests** mirror the component path under `tests/` (e.g. `tests/components/Navbar.test.tsx`). Vitest runs in jsdom with globals enabled — no imports needed for `describe`/`it`/`expect`.

## Styling

Tailwind CSS v4 (PostCSS plugin, no `tailwind.config.ts`). Custom design tokens are defined in `app/globals.css` via `@theme`:

| Token | Usage |
|---|---|
| `primary` | Purple `#C27AFF` — main accent |
| `secondary` | Pink `#FB64B6` — secondary accent |
| `dark` / `light` / `lighter` | Background layers (darkest to lightest) |
| `success` / `error` | Status colors |
| `heading` / `body` | Text colors |

Reusable layout classes defined in `globals.css`: `.page-content`, `.center-content`, `.form-title`.
