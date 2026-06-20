---
name: {Feature Name}
project: {project-name} ({framework})
scope: {medium | large}
slices: {N}
date: {YYYY-MM-DD}
todos:
  - id: s1-{slug}
    content: {Slice 1 goal}
    status: pending
  - id: s2-{slug}
    content: {Slice 2 goal}
    status: pending
---

# {Feature Name} — {Project}

**Project:** {project-name} ({framework})
**Scope:** {Medium | Large} ({N} slices, ~{M} files)
**Date:** {YYYY-MM-DD}

## Overview

{2-3 sentences: what this feature does and why it matters.}

## Tier

**{Free | Freemium | Premium}** — {one-sentence rationale for tier placement}

---

## Slice 1: {Slice Name}

**Goal:** {One sentence describing what this slice delivers.}

### Files

- `path/to/file` — **create**: {what it does}
- `path/to/file` — **modify**: {what changes}

### Tests

- `path/to/test` — {what the test asserts} (unit)
- `path/to/test` — {edge case coverage} (unit)

### States / Edge Cases

- {Empty state behavior}
- {Error state handling}
- {Boundary conditions}

---

## Slice 2: {Slice Name}

**Goal:** {One sentence describing what this slice delivers.}

### Files

- `path/to/file` — **create**: {what it does}
- `path/to/file` — **modify**: {what changes}

### Tests

- `path/to/test` — {what the test asserts} (unit)

---

## Impact Analysis

| Area | Impact |
|------|--------|
| Database | {None / Migration required / New tables} |
| API | {None / New endpoints / Breaking changes} |
| UI | {None / New screens / Component updates} |
| Auth | {None / New permissions / Role changes} |
| Performance | {None / Caching needed / Query optimization} |

## Risks & Considerations

- {Risk 1 and mitigation}
- {Risk 2 and mitigation}

## Out of Scope

- {Explicitly excluded item 1}
- {Explicitly excluded item 2}

---

## Review Checklists

<!-- Include only the sections relevant to this feature. Delete sections that don't apply. -->

### Schema Review
<!-- Include if: DB migrations, new tables/columns, API contract changes -->

- [ ] New tables/columns documented with types and constraints
- [ ] Migration strategy: {backwards compatible | backfill needed | breaking}
- [ ] Index requirements: {list indexes}
- [ ] Foreign keys: {relationships}
- [ ] API contract: {no changes | additive | breaking — versioned?}

### Security Checklist
<!-- Include if: auth changes, user data, external input, new endpoints -->

- [ ] Authentication: {required | not required | N/A}
- [ ] Authorization: {checks needed}
- [ ] Input validation: {where and what}
- [ ] Sensitive data: {PII/secrets handling}
- [ ] Rate limiting: {needed | not needed}
- [ ] OWASP review: {concerns addressed}

### Rollback Plan

- [ ] Feature flagged: {Yes — flag name | No — rationale}
- [ ] Migration reversible: {Yes | No — manual steps needed}
- [ ] Rollback steps: {what to do if deploy fails}
- [ ] Data cleanup: {needed | not needed}

### Feature Flag

- [ ] Gated: {Yes | No} — {rationale}
- [ ] Rollout: {100% | progressive — % ramp}
- [ ] Kill switch: {flag name or N/A}
- [ ] Cleanup: {remove after date/milestone}

### Observability

- [ ] Metrics: {key metrics to track}
- [ ] Alerts: {error scenarios}
- [ ] Logging: {additions needed}
- [ ] Dashboard: {queries to create — see /monitor}

### Dependencies
<!-- Include if: new packages added -->

| Package | Version | License | Notes |
|---------|---------|---------|-------|
| {pkg} | {ver} | {MIT/Apache/etc} | {why needed} |

- [ ] Security advisories checked
- [ ] Bundle size impact: {KB added | N/A}

### Performance
<!-- Include if: data-heavy, latency-sensitive, high-traffic paths -->

- [ ] Query patterns: {expected load}
- [ ] Caching: {strategy or N/A}
- [ ] Pagination: {limits for large datasets}
- [ ] Async: {background job vs sync}

### Accessibility
<!-- Include if: UI changes -->

- [ ] Keyboard nav: {covered}
- [ ] Screen reader: {ARIA labels}
- [ ] Color contrast: {verified}
- [ ] Focus management: {handled}

---

## Implementation Status

- **Status:** PLANNED
- **Current slice:** Slice 1
- **Progress:**
  - [ ] Slice 1: {name}
  - [ ] Slice 2: {name}
- **Last updated:** {YYYY-MM-DD}
- **Deviations:** None yet.
- **Follow-up:** None yet.

## Verification

- [ ] All tests pass
- [ ] Lint passes
- [ ] Manual QA completed
- [ ] PR reviewed
