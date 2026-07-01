---
name: plan
description: Create a scope document from requirements. Plan phase — no code, only planning. Saves to .claude/output/scopes/.
argument-hint: [requirements or feature description]
allowed-tools: Read, Write, Grep, Glob
---

# Plan

Create a **scope document** from requirements. This is the **Plan** phase of:

**Explore → Plan → Implement → Update → Commit → Document**

Do not write code — only produce and save the plan.

## Your task

### 1. Detect context

- Match current directory to a project (check for package.json, Cargo.toml, etc.)
- Note **project name** and **framework/stack**
- Output: `**Project:** {name} ({framework})`

### 2. Detect work type and scope

First, identify the type of work:

| Type | Signals | Template | Notes |
|------|---------|----------|-------|
| **Feature** | "Add", "Create", "Build", new capability | `scope-small.md` or `scope-full.md` | Full planning |
| **Bug fix** | "Fix", "Bug", "Broken", "Doesn't work" | → Suggest `/fix` | Lightweight flow |
| **Refactor** | "Refactor", "Extract", "Clean up", "Reorganize" | `scope-refactor.md` | Safety-focused |
| **Chore** | "Update", "Upgrade", "Config", "CI", deps | `scope-chore.md` | Minimal checklist |
| **Performance** | "Slow", "Optimize", "Speed up" | `scope-perf.md` | Before/after metrics |

**If bug fix:** Suggest `/fix` for simple bugs or `/debug` first if unclear:
```
This looks like a bug fix. For faster iteration:
- Clear issue → Run /fix {description}
- Need investigation → Run /debug {symptoms}
- Complex/risky fix → Continue with /plan
```

Then assess scope size:

| Size | Files | Template variant |
|------|-------|------------------|
| Small | 1-3 files | `-small` or minimal |
| Medium | 4-10 files | full template |
| Large | 10+ files | full template with slices |

State: `**Type:** feature | refactor | chore | performance`
State: `**Scope:** small | medium | large`

### 3. Research and plan

1. Read referenced files; document **current behavior** before proposing changes
2. Fill the appropriate template from `${CLAUDE_PLUGIN_ROOT}/templates/`
3. Identify acceptance criteria and edge cases
4. Check for reusable components (especially for UI work)
5. **Tier classification** — recommend Free / Freemium / Premium with rationale
6. **Test plan** — detect testing framework, list test files and assertions

### 4. Review checklists (include if relevant)

For each applicable checklist, add a section to the scope document.

#### Schema Review (if DB or API changes)
- [ ] New tables/columns documented with types and constraints
- [ ] Migration strategy (backwards compatible? backfill needed?)
- [ ] Index requirements for new queries
- [ ] Foreign key relationships
- [ ] API contract changes (breaking? versioned?)
- [ ] Data validation rules

#### Security Checklist (if auth, user data, or external input)
- [ ] Authentication required for new endpoints
- [ ] Authorization checks (who can access what)
- [ ] Input validation and sanitization
- [ ] Sensitive data handling (PII, secrets, tokens)
- [ ] Rate limiting needed?
- [ ] OWASP top 10 review (injection, XSS, CSRF, etc.)

#### Rollback Plan
- [ ] Can this be feature-flagged?
- [ ] Database migration reversible?
- [ ] How to rollback if deploy fails
- [ ] Data cleanup needed on rollback?

#### Feature Flag Decision
- [ ] Should this be gated? (Yes/No + rationale)
- [ ] Progressive rollout strategy (% ramp, cohorts)
- [ ] Kill switch requirements
- [ ] Flag cleanup plan (when to remove)

#### Observability Hooks (ties into /monitor)
- [ ] Key metrics to track
- [ ] Error scenarios to alert on
- [ ] Logging additions needed
- [ ] Dashboard queries to create

#### Dependencies Audit (if new packages)
- [ ] New dependencies listed with versions
- [ ] License compatibility check
- [ ] Bundle size impact (frontend)
- [ ] Security advisories check
- [ ] Maintenance status (actively maintained?)

#### Performance Considerations (if data-heavy or latency-sensitive)
- [ ] Query patterns and expected load
- [ ] Caching strategy
- [ ] Pagination/limits for large datasets
- [ ] Background job vs sync processing

#### Accessibility (if UI changes)
- [ ] Keyboard navigation
- [ ] Screen reader support (ARIA labels)
- [ ] Color contrast
- [ ] Focus management

### 5. Save the scope

Location: `.claude/output/scopes/{feature-slug}-{project}.md`

Create the directory if needed:
```bash
mkdir -p .claude/output/scopes
```

### 6. Signal next step

For single-slice:
```
Run /implement .claude/output/scopes/{filename}.md
```

For multi-slice:
```
This plan has N slices. Each /implement run handles one slice = one PR.
Run /implement .claude/output/scopes/{filename}.md
```

## Formatting rules

1. **YAML frontmatter first** — name, project, scope, slices, date, todos
2. **Files listed once** — inside their slice section only
3. **No standalone AC section** — express behavior inline unless requirements are ambiguous
4. **Slice sections are flat** — Goal, Files, Tests, and max 3 sub-sections
5. **Impact Analysis is a table** — not prose
6. **Edge cases inside slices** — not as a top-level section
