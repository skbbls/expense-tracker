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

React app with no routing or external state management. `src/App.jsx` is the root; it owns `transactions` state and a module-level `categories` array, and delegates to three components:

- **`Summary`** — receives `transactions`, computes `totalIncome`, `totalExpenses`, and `balance` internally.
- **`TransactionForm`** — owns its own form state (`description`, `amount`, `type`, `category`); calls `onAdd(transaction)` prop when submitted; parses `amount` to `parseFloat` before passing it up.
- **`TransactionList`** — owns filter state (`filterType`, `filterCategory`); receives `transactions` and `categories` as props.

**State shape** — `transactions` is the core array; each entry has `{ id, description, amount, type, category, date }`. `amount` is always a number.

**Data flow** — `App` passes `transactions` down to all three components. `TransactionForm` pushes new transactions up via `onAdd`. There is no persistence; state resets on page reload.

**Categories** — the `categories` array is defined once at module level in `App.jsx` and passed as a prop to both `TransactionForm` and `TransactionList`.
