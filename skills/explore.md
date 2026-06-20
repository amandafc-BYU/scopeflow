---
name: explore
description: Read-only codebase exploration. Use for the Explore phase — read files, answer questions, gather context before planning. No edits.
argument-hint: [what to explore — e.g. "src/auth and session handling"]
allowed-tools: Read, Grep, Glob
context: fork
agent: Explore
---

# Explore

Read-only codebase exploration. This is the **Explore** phase of:

**Explore → Plan → Implement → Update → Commit → Document**

Runs in a forked agent so exploration stays read-only and doesn't fill your main context.

## Your task

1. **Read and analyze** the files or areas the user asked about
2. **Answer questions** about how things work, where code lives, current behavior
3. **Summarize findings** with specific file:line references

## Rules

- Use Read, Grep, Glob only — no Write, Edit, or Bash that modifies files
- If the request is vague, suggest a focused exploration
- Point to files and sections relevant to the user's goal
- Do NOT propose implementation plans — that's for `/prepare`

## Output

- What you explored
- What you found (with file:line references)
- Relevant patterns or conventions discovered

## Next step

When done, tell the user:
```
Run /prepare <requirements> to create a scope document.
```
