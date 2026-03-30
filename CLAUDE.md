# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm run dev      # Start dev server at http://localhost:5173
npm run build    # Production build
npm run lint     # Run ESLint
npm run preview  # Preview production build
```

## Architecture

This is a single-file React app — all logic lives in `src/App.jsx` with styles in `src/App.css`.

**State** (all in `App` component):
- `transactions` — array of `{ id, description, amount, type, category, date }`. Note: `amount` is stored as a string, which causes a known bug where string concatenation is used instead of numeric addition in the income/expense totals.
- Form state: `description`, `amount`, `type`, `category`
- Filter state: `filterType`, `filterCategory`

**Known bug:** `amount` values are strings, so `reduce((sum, t) => sum + t.amount, 0)` concatenates instead of adding — totals and balance are incorrect.

**Data flow:** No persistence — state is in-memory only and resets on page reload. Seed data is hardcoded in the initial `useState` call.
