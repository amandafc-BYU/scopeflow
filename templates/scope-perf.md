---
name: {Performance Improvement}
project: {project-name} ({framework})
type: performance
scope: {small | medium | large}
date: {YYYY-MM-DD}
---

# Performance: {What} — {Project}

**Project:** {project-name} ({framework})
**Type:** Performance
**Scope:** {size}
**Date:** {YYYY-MM-DD}

## Problem

{What is slow and how it impacts users.}

**Symptom:** {Observable behavior — "page takes 5s to load"}
**Impact:** {User/business impact — "users abandon checkout"}
**Frequency:** {How often — "every page load" / "10% of requests"}

## Baseline Metrics

Measure BEFORE making changes:

| Metric | Current | Target | How measured |
|--------|---------|--------|--------------|
| {Load time} | {5s} | {<1s} | {Lighthouse / Network tab} |
| {Query time} | {800ms} | {<100ms} | {EXPLAIN ANALYZE / APM} |
| {Bundle size} | {2MB} | {<500KB} | {build output / bundlesize} |
| {Memory} | {500MB} | {<200MB} | {profiler / metrics} |

## Root Cause Analysis

**Where:** `{file:line or area}`

**Why slow:**
- {Cause 1 — e.g., N+1 queries}
- {Cause 2 — e.g., no caching}
- {Cause 3 — e.g., large payload}

**Evidence:**
```
{Profile output, slow query, flame graph summary}
```

## Approach

{Strategy for improving performance.}

### Option A: {Approach}
- **Effort:** {Low | Medium | High}
- **Impact:** {Expected improvement}
- **Risk:** {What could break}

### Option B: {Alternative if applicable}
- **Effort:** {Low | Medium | High}
- **Impact:** {Expected improvement}
- **Risk:** {What could break}

**Chosen:** {Option} — {rationale}

## Changes

| File | Change | Expected impact |
|------|--------|-----------------|
| `{file}` | {what} | {impact} |

## Caching Strategy

{If applicable}

- **What to cache:** {data/computation}
- **Cache location:** {memory / Redis / CDN / browser}
- **TTL:** {duration}
- **Invalidation:** {when/how to bust cache}

## Verification

### Performance tests
- [ ] Baseline recorded before changes
- [ ] Same test after changes
- [ ] Improvement measured and documented

### Regression tests
- [ ] Existing tests pass
- [ ] No behavior changes
- [ ] Edge cases still work

### Production validation
- [ ] Monitor metrics after deploy
- [ ] No increase in errors
- [ ] User-facing improvement confirmed

## Results

**After optimization:**

| Metric | Before | After | Improvement |
|--------|--------|-------|-------------|
| {metric} | {old} | {new} | {X% faster} |

## Observability

- [ ] Add timing metrics for ongoing monitoring
- [ ] Set up alerts for regression
- [ ] Dashboard query created (see `/monitor`)

---

## Implementation Status

- **Status:** PLANNED
- **Progress:** [ ] Baseline [ ] Implement [ ] Measure [ ] Verify
- **Last updated:** {YYYY-MM-DD}
