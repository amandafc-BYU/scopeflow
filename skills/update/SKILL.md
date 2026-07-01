---
name: update
description: Update a scope document with current session progress. Keeps the living scope in sync with implementation reality.
argument-hint: [optional — path to scope file]
allowed-tools: Read, Write, Edit, Bash, Grep, Glob
---

# Update

Update a scope document with progress from the current session. This keeps a **living scope** that tracks implementation reality.

Use after `/implement`, after manual coding, or after debugging.

## Your task

### 1. Locate the scope file

- If path provided, use it
- Otherwise, list `.claude/output/scopes/` and use most recent or ask

### 2. Gather session context

```bash
git diff --name-only main
git log --oneline main..HEAD
```

Review conversation for:
- Which acceptance criteria were worked on
- Which files were created/modified
- Blockers or discoveries

### 3. Compare against scope

Cross-reference:
- Which **acceptance criteria** are now satisfied?
- Which **files** were actually modified?
- Any **deviations** from the plan?
- Any **follow-up work** discovered?

Distinguish:
- **[SCOPE CHANGE]** — functional spec changes (requirements, AC, business rules)
- Technical deviations — different approach, different files (normal, no prefix)

### 4. Update the scope file

#### Acceptance Criteria
- Check off `[x]` criteria confirmed by git diff
- Leave unchecked if not clearly met

#### Implementation Status
- **Progress:** Check off `[x]` completed items
- **Current slice:** Next incomplete slice, or `COMPLETE`
- **Status:** `PLANNED` | `IN PROGRESS` | `IMPLEMENTED`
- **Last updated:** Today's date
- **Deviations:** One line per deviation (prefix functional changes with `[SCOPE CHANGE]`)
- **Follow-up:** Tech debt or future work items

Do NOT modify the **Verification** section.

### 5. Print summary

```
## Scope updated: {filename}

**Status:** {status}
**Acceptance criteria:** {X}/{total} met
**Progress:** {X}/{total} complete
**Deviations:** {N} ({M} scope changes)
**Follow-up items:** {N}
```

## Rules

- Only check off what you can confirm from git diff
- Preserve original scope content
- When in doubt, leave unchecked
