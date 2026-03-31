
# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm run dev      # Start dev server at http://localhost:5173
npm run build    # Production build
npm run lint     # Run ESLint
npm run preview  # Preview production build
```

## Deploy

Use the `/deploy` skill to deploy. It runs lint → build → pushes to the `staging` branch on GitHub.

## Architecture

React + Vite app. All styles are in `src/App.css`.

**Component tree:**
- `App` — holds `transactions` state, `handleAdd` (useCallback), and `handleDelete` (useCallback). Passes data down to children.
  - `Summary` — receives `transactions`, computes totalIncome, totalExpenses, and balance internally.
  - `TransactionForm` — owns its own form state (`description`, `amount`, `type`, `category`). Calls `onAdd` prop with a new transaction object on submit. Converts `amount` to a float before passing up.
  - `TransactionList` — receives `transactions`, owns filter state (`filterType`, `filterCategory`) internally.
  - `SpendingChart` — receives `transactions`, aggregates expenses by category, renders a recharts BarChart with a distinct color per bar.

**Shared constants:** `src/constants.js` exports `CATEGORIES` — the canonical list of transaction categories used by both `TransactionForm` and `TransactionList`.

**Styling:** Dark premium theme. CSS custom properties in `src/App.css`. Fonts: Syne (headings), DM Mono (numbers), DM Sans (body) via Google Fonts in `index.html`.

**Data flow:** No persistence — state is in-memory only and resets on page reload. Seed data is hardcoded in `App`'s initial `useState` call. `amount` is stored as a number.

## Dependencies

- `recharts` — bar chart
- `react-is` — peer dependency required by recharts
