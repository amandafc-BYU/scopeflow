---
name: fix
description: Lightweight bug fix workflow. Faster than full /plan — for known issues with clear fixes.
argument-hint: [bug description or issue link]
allowed-tools: Read, Write, Edit, Bash, Grep, Glob
---

# Fix

Lightweight workflow for bug fixes. Use when:
- The issue is understood (no deep investigation needed)
- The fix is scoped (1-3 files)
- You want to move fast without full planning overhead

For complex or unclear bugs, use `/debug` first.

## Your task

### 1. Confirm understanding

State clearly:
```markdown
**Bug:** {What's broken}
**Expected:** {What should happen}
**Actual:** {What happens instead}
**Repro:** {How to reproduce}
```

If any of these are unclear, run `/debug` first.

### 2. Locate the problem

```bash
# Find relevant code
grep -rn "keyword" src/

# Check recent changes if regression
git log --oneline --since="1 week ago" -- path/to/area/
```

Identify:
- **File(s):** Where the bug lives
- **Root cause:** Why it's broken (one sentence)

### 3. Plan the fix

Minimal scope doc (or skip if trivial):

```markdown
# Fix: {Bug Title}

**Date:** {YYYY-MM-DD}
**Ticket:** {link if any}

## Problem
{One sentence}

## Root Cause
{Where and why}

## Fix
- `{file}` — {what to change}

## Tests
- `{test file}` — {what to verify}

## Verification
- [ ] Bug no longer reproduces
- [ ] Tests pass
- [ ] No regressions in related area
```

Save to `.claude/output/fixes/{bug-slug}-{date}.md` if you want a record.

### 4. Implement the fix

- Make the minimal change needed
- Don't refactor unrelated code
- Don't add features

### 5. Verify

```bash
# Run tests
npm test  # or project's test command

# Run lint
npm run lint  # or project's lint command

# Manual verification
# {reproduce the bug scenario — should now work}
```

### 6. Commit

Use conventional commit format:
```
fix(scope): brief description

Fixes #123

Root cause: {one line}
```

## When to upgrade to full /plan

Escalate if you discover:
- Fix requires 4+ files
- Schema or API changes needed
- Security implications
- Risk of regression is high
- Multiple issues tangled together

```
This needs more planning. Run /plan {requirements}
```

## Quick fix checklist

- [ ] Bug understood and reproducible
- [ ] Root cause identified
- [ ] Fix is minimal and focused
- [ ] Tests cover the fix
- [ ] Manual verification done
- [ ] No regressions introduced
- [ ] Committed with clear message
