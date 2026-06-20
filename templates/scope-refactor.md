---
name: {Refactor Name}
project: {project-name} ({framework})
type: refactor
scope: {small | medium | large}
date: {YYYY-MM-DD}
---

# Refactor: {What} — {Project}

**Project:** {project-name} ({framework})
**Type:** Refactor
**Scope:** {size} (~{N} files)
**Date:** {YYYY-MM-DD}

## Goal

{One sentence: what you're improving and why.}

## Before

{Current state — structure, patterns, issues.}

```
{Current code structure or architecture diagram}
```

**Problems:**
- {Issue 1}
- {Issue 2}

## After

{Target state — new structure, patterns, improvements.}

```
{New code structure or architecture diagram}
```

**Improvements:**
- {Benefit 1}
- {Benefit 2}

## Files

| File | Action | Change |
|------|--------|--------|
| `path/to/file` | modify | {what changes} |
| `path/to/file` | create | {new file purpose} |
| `path/to/file` | delete | {why removing} |
| `path/to/file` | rename | {old} → {new} |

## Safety Checklist

- [ ] All existing tests pass before starting
- [ ] No behavior changes (pure refactor)
- [ ] Types/interfaces preserved or migrated
- [ ] Imports updated across codebase
- [ ] No dead code left behind
- [ ] Git history preserves blame (use `git mv` for renames)

## Test Coverage

**Existing tests:** {list tests that cover this area}

- [ ] Tests pass before refactor
- [ ] Tests pass after refactor
- [ ] No test changes needed (behavior unchanged)

Or if tests need updating:
- [ ] Test file renames/moves
- [ ] Import updates in tests

## Verification

- [ ] `npm test` passes (all tests)
- [ ] `npm run lint` passes
- [ ] `npm run build` succeeds
- [ ] Manual smoke test of affected features
- [ ] No runtime errors in console

## Rollback

**Risk:** Low | Medium | High
**Rollback:** {Revert commit | More complex steps}

## Out of Scope

- {Do NOT change behavior}
- {Do NOT add features}
- {Do NOT fix bugs — separate PR}

---

## Implementation Status

- **Status:** PLANNED
- **Progress:** [ ] {step 1} [ ] {step 2}
- **Last updated:** {YYYY-MM-DD}
