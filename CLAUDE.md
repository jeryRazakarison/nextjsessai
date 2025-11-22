# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Next.js 15+ App Router dashboard application with TypeScript, Tailwind CSS, PostgreSQL, and NextAuth.js (beta). This is a starter template from the official Next.js App Router Course.

## Commands

```bash
pnpm dev          # Start dev server with Turbopack
pnpm build        # Production build
pnpm start        # Start production server
```

## Architecture

**Stack:** Next.js App Router, TypeScript (strict), Tailwind CSS, PostgreSQL (raw SQL), NextAuth v5 beta

**Key directories:**
- `app/lib/` - Database queries (`data.ts`), types (`definitions.ts`), utilities (`utils.ts`)
- `app/ui/` - Reusable components organized by feature (dashboard/, invoices/, customers/)
- `app/seed/route.ts` - Database seeding endpoint (GET /api/seed)

**Data layer:**
- Direct PostgreSQL queries using `postgres` library (not an ORM)
- All queries in `app/lib/data.ts` with parameterized SQL
- Connection via `POSTGRES_URL` environment variable with SSL

**Database tables:** users, customers, invoices, revenue

**Component patterns:**
- Server Components by default (data fetching in components)
- Client Components only where needed (marked with 'use client')
- Skeleton loading states with shimmer animation

**Path alias:** `@/*` maps to project root (e.g., `@/app/ui/button`)

## Environment Variables

Required in `.env.local` (see `.env.example`):
- `POSTGRES_URL` - PostgreSQL connection string
- `AUTH_SECRET` - NextAuth secret (generate with `openssl rand -base64 32`)
- `AUTH_URL` - Auth URL (http://localhost:3000/api/auth for local)

## Database Setup

Seed the database by visiting `/api/seed` after configuring PostgreSQL connection.
