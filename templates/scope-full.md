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
