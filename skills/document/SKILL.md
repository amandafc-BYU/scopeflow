---
name: document
description: Create feature documentation from the completed scope. Summary, tests, manual steps, troubleshooting.
argument-hint: [optional — scope path or feature name]
allowed-tools: Read, Write, Bash, Grep, Glob
---

# Document

Create feature documentation after implementation. This is the **Document** phase of:

**Explore → Plan → Implement → Update → Commit → Document**

## Your task

### 1. Gather context

- Read scope doc if path provided, otherwise infer from git history
- Read the template: `$SCOPEFLOW_DIR/templates/feature-doc.md`
- Identify project stack and conventions

### 2. Fill the template

Include:

**Overview** — What the feature does for users (no implementation details)

**Prerequisites** — Env vars, services, permissions needed

**Usage** — Step-by-step for primary use cases

**Configuration** — Settings table if applicable

**API Reference** — If the feature exposes APIs

**Testing**
- How to run automated tests
- Manual testing steps with expected results

**Troubleshooting** — Table: symptom | cause | solution

**Related** — Links to scope doc, PR, ticket

### 3. Apply technical writing best practices

- Active voice, present tense
- Short sentences, one idea per paragraph
- Imperative mood for instructions ("Click...", "Run...")
- Consistent terminology
- No jargon without definition

### 4. Save

Prefer repository location:
- `docs/features/{feature-name}.md`
- Or `docs/{feature-name}.md`

If standalone artifact needed:
- `.claude/output/docs/{YYYY-MM-DD}-{feature-slug}.md`

### 5. Confirm

Tell the user what was created and where.

## Output structure

```markdown
# Feature Name

{Overview paragraph}

## Prerequisites
## Usage
## Configuration
## API Reference
## Testing
## Troubleshooting
## Related

---
*Last updated: {date}*
```
