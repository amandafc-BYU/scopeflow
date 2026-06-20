---
name: implement
description: Implement a feature from a scope document. Code against the plan, run tests, fix failures.
argument-hint: [path to scope file — e.g. .claude/output/scopes/feature-project.md]
allowed-tools: Read, Write, Edit, Bash, Grep, Glob
---

# Implement

Implement the feature from a scope document. This is the **Implement** phase of:

**Explore → Plan → Implement → Update → Commit → Document**

## Your task

### 1. Read the scope file

Resolve the path:
- If relative, check `.claude/output/scopes/` first
- Read the scope document fully

### 2. Implement

- Follow **Files** and **Approach** sections
- If multi-slice, implement **one slice** per invocation
- Ask which slice if unclear
- Respect acceptance criteria and business rules
- Address risks noted in the scope

### 3. Verify

- Run the project's test suite (or tests from the plan)
- Fix any failures before proceeding
- Run lint if defined; fix violations
- Confirm acceptance criteria are met

### 4. Update the scope

After implementation, update these sections:
- **Progress** — check off completed items
- **Status** — set to `IN PROGRESS` or `IMPLEMENTED`
- **Deviations** — note any changes from the plan
- **Last updated** — today's date

## Rules

- Do NOT commit or create a PR — use `/commit` for that
- One slice = one implementation session
- Tests must pass before marking anything complete

## Next step

When implementation is complete:
```
Run /update to sync the scope, then /commit to ship.
```
