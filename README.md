# Aegis Insurance Platform

Aegis is a Next.js application that demonstrates a commission-protection workflow for insurance agencies and agents. It models how commissions are split into **safe** and **vaulted** balances, how vaults **vest over time**, and how **chargebacks/advances** create debt that can be repaid via garnishment.

This repository is currently a front-end demo powered by local mock JSON data.

## Table of Contents

- [What This Project Does](#what-this-project-does)
- [Core Concepts](#core-concepts)
- [Key Features](#key-features)
- [Tech Stack](#tech-stack)
- [Application Routes](#application-routes)
- [Project Structure](#project-structure)
- [Data Model and Mock Data](#data-model-and-mock-data)
- [Local Development](#local-development)
- [Available Scripts](#available-scripts)
- [Deployment](#deployment)
- [Known Baseline Issues](#known-baseline-issues)

## What This Project Does

The app provides two dashboard experiences:

1. **Agency view** for owners/managers to monitor aggregate risk and configure operations.
2. **Agent view** for individual producers to track available funds, vaulting, vesting, and debt.

It is designed as an interactive product demo with a realistic information architecture and business flow.

## Core Concepts

- **Safe balance**: funds immediately available to spend.
- **Vaulted balance**: withheld funds that protect against future chargebacks.
- **Vesting**: gradual release of vaulted funds over time.
- **Debt**: obligations caused by chargebacks or advances.
- **Garnishment**: automatic repayment of debt from future commissions.

## Key Features

### Landing Experience

- Marketing-style homepage at `/` with feature highlights and navigation to demos.

### Agency Dashboard

- Portfolio-level metrics for vaulted, safe, and debt balances.
- Agent-level table and detail views.
- Commission trend and performance visualizations.
- Real-time simulation/risk components.
- Dedicated pages for:
  - debt management
  - vault rule configuration
  - vesting management

### Agent Dashboard

- Personal financial overview cards (safe, vaulted, debt).
- Debt alerts and debt history view.
- Commission and vault breakdown charts.
- Book-of-business display.
- Interactive vault visualizer.
- Recent commissions and vesting-linked vault list.

## Tech Stack

- **Framework**: Next.js 15.5 (App Router)
- **Language**: TypeScript
- **UI**: React 18, Tailwind CSS, shadcn/ui, Radix UI primitives
- **Forms/Validation**: React Hook Form + Zod
- **Charts**: Recharts
- **Icons**: Lucide React
- **Linting**: ESLint

## Application Routes

### Public

- `/` — Landing page

### Agency

- `/agency` — Agency command center
- `/agency/agents/[id]` — Agent detail/performance page
- `/agency/debts` — Debt management
- `/agency/vault-rules` — Vault rule management
- `/agency/vesting` — Upcoming vestings

### Agent

- `/agent` — Agent dashboard (demo agent)
- `/agent/debts` — Agent debt management

## Project Structure

```text
src/
├── app/
│   ├── page.tsx                    # Landing page
│   ├── agency/                     # Agency dashboard routes
│   │   ├── page.tsx
│   │   ├── agents/[id]/page.tsx
│   │   ├── debts/page.tsx
│   │   ├── vault-rules/page.tsx
│   │   └── vesting/page.tsx
│   ├── agent/                      # Agent dashboard routes
│   │   ├── page.tsx
│   │   └── debts/page.tsx
│   └── layout.tsx                  # Global layout/providers
├── components/
│   ├── agency/                     # Agency-focused UI/features
│   ├── agent/                      # Agent-focused UI/features
│   └── ui/                         # Reusable shadcn/ui primitives
├── data/                           # Mock domain data (JSON)
│   ├── agents.json
│   ├── commissions.json
│   ├── debts.json
│   ├── vault-rules.json
│   └── vesting-schedule.json
├── hooks/
└── lib/
    ├── types.ts
    └── utils.ts
```

## Data Model and Mock Data

The UI is driven by local JSON data under `src/data/`.

Primary datasets:

- `agents.json`: profile/status and balance/risk metadata per agent
- `commissions.json`: gross/safe/vaulted values, policy metadata, status, dates
- `debts.json`: active and historical debt records (chargebacks, advances)
- `vault-rules.json`: split percentages and vesting configuration
- `vesting-schedule.json`: pending/completed vesting events

There is also a shared TypeScript model layer in `src/lib/types.ts` that represents the intended domain entities.

## Local Development

### Prerequisites

- Node.js 18+ (Node 20+ recommended)
- npm 9+

### Setup

```bash
npm install
```

### Run in development

```bash
npm run dev
```

Then open [http://localhost:3000](http://localhost:3000).

## Available Scripts

```bash
npm run dev      # Start dev server
npm run build    # Production build
npm run start    # Start production server (after build)
npm run lint     # Lint the codebase
```

## Deployment

A public deployment was previously provided at:

- https://aegis-insurance.pages.dev/

If deploying this repository yourself, standard Next.js deployment targets (Vercel, Cloudflare-compatible setups, etc.) apply.

## Known Baseline Issues

Current repository baseline includes pre-existing lint and build issues unrelated to this README update:

- `npm run lint` reports existing TypeScript/ESLint violations in multiple app/component files.
- `npm run build` may fail in restricted/offline environments because `next/font` attempts to fetch Inter from Google Fonts (`fonts.googleapis.com`).

These are existing project conditions and not introduced by this documentation change.
