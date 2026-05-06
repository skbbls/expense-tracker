# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm run dev       # start dev server at http://localhost:5173
npm run build     # production build
npm run preview   # preview production build locally
npm run lint      # run ESLint
```

There is no test suite.

## Architecture

This is a single-file React app. All state, logic, and UI live in `src/App.jsx` — there are no sub-components, routing, or external state management.

**State shape** — `transactions` is the core array; each entry has `{ id, description, amount, type, category, date }`. `amount` is stored as a string (known bug — arithmetic on it produces string concatenation instead of numeric sums).

**Data flow** — everything is derived inline from `transactions` on each render: `totalIncome`, `totalExpenses`, `balance`, and `filteredTransactions`. There is no persistence; state resets on page reload.

**Categories** — the `categories` array is the single source of truth for both the add-form dropdown and the filter dropdown.

**Intentional issues** — per the README this starter has a known bug (amount string/number mismatch), poor UI, and messy code. These are meant to be fixed during the course.
