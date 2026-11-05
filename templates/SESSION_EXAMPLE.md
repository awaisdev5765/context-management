# SESSION — storefront (filled example)

Updated: 2026-01-15          Branch: feat/checkout

## Project
E-commerce storefront (React 18 + Vite, TypeScript, Tailwind v3, zod).
Runs: `npm run dev` → localhost:5173 · Tests: `npm test` (vitest) · Lint: `npm run lint`

## Current state
- ✅ DONE: Cart state + reducer (src/store/cart.ts); product list page renders from /api/products
- ✅ DONE: Checkout button POSTs to /api/orders and redirects on success
- 🔨 IN PROGRESS: Order error handling — src/components/CheckoutButton.tsx, step 3 of 4
  (done: try/catch wrap; next: toast component, then empty-cart guard)
- ❌ BLOCKED: POST /api/orders returns 422 "variant_id required" — backend expects variantId, we send productId.
  Attempts: 1) renamed payload field — still 422; 2) sent both — duplicate key error.

## Decisions made (do not relitigate)
- No state library — React context + reducers is enough at this size (2026-01-10)
- All API errors surface via toast, never alert() — matches src/components/Toast.tsx pattern (2026-01-12)
- REVERSED 2026-01-14: was "no router lib" — we adopted react-router v6 for /orders/* routes

## Next steps (in order)
1. Fix order payload: send `variantId: item.variant.id` in src/api/orders.ts
2. Add toast on order failure (use existing Toast component)
3. Guard: disable checkout when cart is empty
4. Add vitest case for failed order → toast shown

## Gotchas
- /api/* is a mock server (`npm run mock`); it restarts with empty data on save
- Tailwind v3 — do NOT use v4-only syntax (no @theme, no CSS-first config)
- Tests run with NODE_ENV=test which points fetch at fixtures/, not the mock server
