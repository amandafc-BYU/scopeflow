---
name: scopeflow
description: Structured feature development workflow — Explore → Plan → Implement → Update → Commit → Document. Use when starting new features, fixing bugs with scope docs, or following the explore-first best practice.
allowed-tools: Read, Write, Edit, Bash, Grep, Glob
---

# Scopeflow

Structured feature development workflow for Claude Code.

## When to use

- Starting a new feature (run `/explore` then `/prepare`)
- Implementing from a scope document (`/implement`)
- Updating progress mid-session (`/update`)
- Committing and creating a PR (`/commit`)
- Creating feature documentation (`/document`)

## The workflow

```
/explore → /prepare → /implement → /update → /commit → /document
```

1. **Explore** — Read-only codebase discovery before planning
2. **Prepare** — Create a scope document from requirements
3. **Implement** — Code against the scope, run tests, fix failures
4. **Update** — Sync the scope doc with implementation reality
5. **Commit** — Commit changes and create a PR
6. **Document** — Generate feature docs from the completed scope

## Quick start

```
/explore src/auth and how we handle sessions
```
Then:
```
/prepare Add OAuth login with Google
```
Then:
```
/implement .claude/output/scopes/oauth-login-project.md
```

## Commands

| Command | Purpose |
|---------|---------|
| `/explore <area>` | Read-only exploration of codebase |
| `/prepare <requirements>` | Create scope document |
| `/implement <scope-path>` | Implement from scope doc |
| `/update [scope-path]` | Update scope with progress |
| `/commit [ticket-ref]` | Commit and create PR |
| `/document [scope-path]` | Create feature documentation |

## Templates

This plugin includes templates in `templates/`:
- `scope-small.md` — For small scopes (1-3 files)
- `scope-full.md` — For medium/large scopes
- `pr-template.md` — PR description template
- `feature-doc.md` — Feature documentation template

Skills reference these via `$SCOPEFLOW_DIR/templates/`.
