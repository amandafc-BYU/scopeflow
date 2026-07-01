---
name: commit
description: Commit changes and create a PR with context from the scope document.
argument-hint: [optional — ticket ref, e.g. DX-523]
allowed-tools: Read, Bash, Grep, Glob
---

# Commit

Commit changes and create a pull request. This is the **Commit** phase of:

**Explore → Plan → Implement → Update → Commit → Document**

## Your task

### 1. Review changes

```bash
git status
git diff
```

Identify what will be committed.

### 2. Commit

- Use **conventional commits** style: `feat(scope): description`
- Include ticket ref if provided (in commit body or PR)
- Stage only files for this feature — no unrelated changes

Example:
```bash
git add src/auth/ tests/auth/
git commit -m "feat(auth): add Google OAuth login

Implements OAuth flow with session persistence.
Ticket: DX-523"
```

### 3. Create PR

Use the PR template from `${CLAUDE_PLUGIN_ROOT}/templates/pr-template.md`:

1. Read the template
2. Fill in from changes and scope document
3. Push and create PR

```bash
git push -u origin HEAD
gh pr create --title "feat(auth): add Google OAuth login" --body-file /tmp/pr-body.md
```

Or construct inline:
```bash
gh pr create --title "..." --body "## Summary
..."
```

### 4. Link to scope

Include in PR description:
```
## Scope Document
.claude/output/scopes/{feature-project}.md
```

## PR template structure

- **Summary** — What and why
- **Changes** — Bullet list
- **Scope Document** — Path to scope
- **Testing** — Automated + manual steps
- **Screenshots** — If UI changes
- **Related** — Tickets, dependencies
- **Checklist** — Standards verification

## Next step

After PR is merged:
```
Run /document to create feature documentation.
```
