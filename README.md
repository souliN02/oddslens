# OddsLens

A self-hosted football odds tracker that snapshots bookmaker odds over time,
computes no-vig consensus probabilities, and flags outlier prices.

> 🚧 Work in progress. Built in phases — see [`SPEC.md`](./SPEC.md) for the full
> product spec and [`CLAUDE.md`](./CLAUDE.md) for working conventions. The full
> README (architecture diagram, engineering decisions, live demo) lands in the
> final polish phase.

## Stack

Next.js (App Router) · TypeScript strict · Tailwind CSS · shadcn/ui · Drizzle +
Neon Postgres · Zod · Recharts · Vitest · GitHub Actions + Vercel.

## Local setup

```bash
npm install
cp .env.example .env   # fill in values as later phases need them
npm run dev            # http://localhost:3000
```

## Scripts

```bash
npm run dev          # local dev server
npm run build        # production build
npm run lint         # eslint
npm run typecheck    # tsc --noEmit
npm test             # vitest run
npm run format       # prettier --write .
```

## Disclaimer

Educational analytics project. Not betting advice.
