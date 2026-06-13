# CLAUDE.md - OddsLens

Football odds tracker. Full product spec lives in `SPEC.md` - read it before any task. Build strictly within the MVP scope in SPEC.md section 2; suggest extras, do not build them.

## Commands

```
npm run dev          # local dev server
npm run build        # production build
npm run lint         # eslint
npm run typecheck    # tsc --noEmit
npm test             # vitest run
npm run db:generate  # drizzle-kit generate migrations
npm run db:migrate   # apply migrations
npm run db:seed      # seed local/dev DB from tests/fixtures/odds-response.json
```

## Definition of done (every task)

1. `npm run typecheck`, `npm run lint`, and `npm test` all pass locally
2. New logic has tests (odds math is always test-first)
3. UI changes handle loading, empty, and error states
4. Commit with a conventional commit message (`feat:`, `fix:`, `test:`, `chore:`, `docs:`)

## Hard rules

- **Never call The Odds API during development or tests.** Use `tests/fixtures/odds-response.json`. The free tier has ~500 credits/month and the scheduled job needs almost all of them (SPEC.md section 4).
- **Never commit secrets.** `.env` is gitignored; keep `.env.example` updated when adding variables.
- TypeScript strict mode, no `any`, no `@ts-ignore`. If a type is hard, fix the type.
- All external data passes through Zod schemas in `src/lib/odds-api.ts` before touching the rest of the app.
- Odds values are `numeric` in Postgres and strings in Drizzle results; convert deliberately in one place.
- Odds math lives only in `src/lib/odds-math.ts` as pure functions. No math inline in components.
- Server components for data reads by default; client components only where interactivity requires it (charts, toggles, filters).
- Keep components small and colocated. No premature abstraction, no extra dependencies without asking.
- Timezone: display kickoff times in Europe/Copenhagen.

## Project structure

```
src/
  app/                  # routes: /, /match/[id], /about, /api
  components/           # shared UI
  db/                   # drizzle schema, client, seed
  lib/
    odds-api.ts         # The Odds API client + Zod schemas (only file that knows the external shape)
    odds-math.ts        # pure functions: implied, overround, noVig, consensus, edge, bestPrice
tests/
  fixtures/odds-response.json
.github/workflows/      # ci.yml, snapshot.yml
```

## Workflow

- One phase from SPEC.md section 12 per session, on a feature branch, merged via PR with green CI.
- Plan before implementing on any multi-file change; show the plan first.
- When a phase is done, update the README if behavior or setup changed.
