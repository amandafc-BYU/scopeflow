---
name: debug
description: Investigate and debug an issue. Capture symptoms, form hypotheses, find root cause. Can be standalone or mid-implementation.
argument-hint: [issue description — e.g. "login fails after password reset"]
allowed-tools: Read, Write, Edit, Bash, Grep, Glob
---

# Debug

Systematic investigation of an issue. Can be used:
- **Standalone** — When a bug is reported and you need to investigate
- **Mid-flow** — When implementation reveals an unexpected issue

## Your task

### 1. Capture the issue

Document in a debug log (`.claude/output/debug/{issue-slug}-{date}.md`):

```markdown
# Debug: {Issue Title}

**Date:** {YYYY-MM-DD}
**Status:** INVESTIGATING | ROOT_CAUSE_FOUND | RESOLVED
**Related scope:** {path to scope doc if mid-flow, or N/A}

## Symptoms

- {What is happening}
- {What should be happening}
- {When it started / what changed}

## Reproduction

1. {Step to reproduce}
2. {Step to reproduce}
3. {Observed behavior}

**Reproduces:** Always | Sometimes | Unclear
**Environment:** {local | staging | production | all}
```

### 2. Gather evidence

```bash
# Check recent changes
git log --oneline -20
git diff HEAD~5

# Search for relevant code
grep -r "error pattern" src/

# Check logs if available
tail -100 logs/app.log 2>/dev/null
```

Look for:
- Recent changes in related areas
- Error messages and stack traces
- Relevant log entries
- Environment differences

### 3. Form hypotheses

List possible causes ranked by likelihood:

```markdown
## Hypotheses

| # | Hypothesis | Likelihood | How to verify |
|---|------------|------------|---------------|
| 1 | {Most likely cause} | High | {Check X} |
| 2 | {Second possibility} | Medium | {Check Y} |
| 3 | {Less likely} | Low | {Check Z} |
```

### 4. Investigate systematically

For each hypothesis:
1. State what you're checking
2. Run the verification
3. Document findings
4. Update hypothesis ranking

```markdown
## Investigation Log

### Hypothesis 1: {description}
**Checking:** {what and how}
**Result:** {what you found}
**Verdict:** Confirmed | Ruled out | Inconclusive
```

### 5. Identify root cause

When found:

```markdown
## Root Cause

**What:** {The actual cause}
**Where:** `{file:line}`
**Why:** {How this caused the symptoms}
**When introduced:** {commit/date if known}
```

### 6. Determine fix path

```markdown
## Fix

**Approach:** {How to fix}
**Files:** 
- `{file}` — {change}

**Risk:** Low | Medium | High
**Verification:** {How to confirm fix works}
```

### 7. Hand off or fix

**If standalone:** 
- Create a `/fix` or small scope doc
- Or fix directly if trivial

**If mid-flow:**
- Update the scope doc with findings
- Add to Deviations if plan changed
- Continue implementation

## Output

Always save the debug log:
```bash
mkdir -p .claude/output/debug
```

Print summary:
```
## Debug: {title}
**Status:** {status}
**Root cause:** {one-line summary}
**Next:** {/fix, continue /implement, or needs more info}
```

## Tips

- **Binary search:** If issue is in a range of commits, use `git bisect`
- **Isolate variables:** Change one thing at a time
- **Check assumptions:** The bug is often in the code you're sure is correct
- **Fresh eyes:** Describe the problem out loud — often reveals the answer
- **Time-box:** If stuck after 30 min, step back and reassess hypotheses
