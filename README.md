# Scopeflow

Structured feature development workflow for Claude Code.

**Explore → Plan → Implement → Update → Commit → Document**

Stop coding without a plan. Scopeflow enforces the [Claude Code best practice](https://claude.ai/code/docs/best-practices#explore-first-then-plan-then-code) of exploring first, then planning, then coding — with living scope documents that track progress, deviations, and follow-up work.

## Why Scopeflow?

Without structure, AI coding sessions drift:
- Features creep beyond the original ask
- Deviations from the plan go undocumented
- Handoffs lose context
- PRs lack clear scope

Scopeflow fixes this with **living scope documents** — plans that update as implementation reveals reality, creating a clear audit trail from requirements to shipped code.

## Install

```bash
git clone https://github.com/edifi-ventures/scopeflow.git ~/.claude/skills/scopeflow
```

Or add to a project:
```bash
git clone https://github.com/edifi-ventures/scopeflow.git .claude/skills/scopeflow
```

## The Workflow

### 1. `/explore` — Understand before you plan
Read-only exploration. Runs in a forked agent so your main context stays clean.

```
/explore src/auth and how sessions are handled
```

### 2. `/plan` — Create a scope document
Turn requirements into a structured plan with acceptance criteria, file lists, and test plans.

```
/plan Add Google OAuth login with session persistence
```

Output: `.claude/output/scopes/google-oauth-myproject.md`

### 3. `/implement` — Code against the plan
Execute slice by slice. Tests run automatically. Failures get fixed before moving on.

```
/implement .claude/output/scopes/google-oauth-myproject.md
```

### 4. `/update` — Keep the scope living
After implementing (or mid-session), sync the scope doc with reality: what's done, what deviated, what's left.

```
/update
```

### 5. `/commit` — Ship with context
Commit and create a PR with a description derived from the scope document.

```
/commit DX-523
```

### 6. `/document` — Create feature docs
Generate user/developer documentation from the completed scope.

```
/document
```

### 7. `/monitor` — Set up observability
Configure monitoring, create dashboard queries, set up alerts.

```
/monitor auth failures and login patterns
```

Supports: Sentry, Metabase, PostgreSQL, Datadog, PostHog, Prometheus

## Scope Document Structure

Every scope document includes:

- **Overview** — What and why (one sentence)
- **Acceptance Criteria** — Checkable requirements
- **Files** — What to create/modify
- **Tests** — Unit tests for each criterion
- **Tier** — Free / Freemium / Premium classification
- **Implementation Status** — Progress, deviations, follow-up

### Small vs Large Scopes

- **Small** (1-3 files): Minimal template, single slice
- **Medium** (4-10 files): Full template
- **Large** (10+ files): Full template with multiple slices (one PR per slice)

## Example Scope Document

```markdown
---
name: Google OAuth Login
project: myapp (Next.js)
scope: medium
slices: 2
date: 2024-01-15
todos:
  - id: s1-auth
    content: OAuth provider and callback
    status: pending
  - id: s2-session
    content: Session persistence
    status: pending
---

# Google OAuth Login — myapp

**Scope:** Medium (2 slices, ~6 files)

## Overview
Add Google OAuth so users can sign in without passwords.

## Slice 1: OAuth Provider
**Goal:** User can click "Sign in with Google" and authenticate.

### Files
- `src/auth/google.ts` — **create**: OAuth client setup
- `src/pages/api/auth/callback.ts` — **create**: OAuth callback handler
- `src/components/LoginButton.tsx` — **modify**: Add Google option

### Tests
- `src/auth/__tests__/google.test.ts` — OAuth flow redirects correctly
- `src/auth/__tests__/google.test.ts` — Callback exchanges code for token

## Implementation Status

- **Status:** PLANNED
- **Progress:** [ ] Slice 1  [ ] Slice 2
- **Deviations:** None yet.
- **Follow-up:** None yet.
```

## Philosophy

1. **Plans are living documents** — They evolve as implementation reveals reality
2. **Deviations are expected** — Document them, don't hide them
3. **One slice = one PR** — Keep changes reviewable
4. **Tests are required** — Every acceptance criterion has a test
5. **Context survives handoffs** — The scope doc is the source of truth

## Skills Reference

| Command | Phase | What it does |
|---------|-------|--------------|
| `/explore` | Explore | Read-only codebase discovery |
| `/plan` | Plan | Create scope document from requirements |
| `/implement` | Implement | Code against the scope, run tests |
| `/update` | Update | Sync scope with implementation progress |
| `/commit` | Commit | Commit changes and create PR |
| `/document` | Document | Generate feature documentation |
| `/monitor` | Ops | Set up monitoring, dashboards, and alerts |

## License

MIT — Edifi Ventures
