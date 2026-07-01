---
name: monitor
description: Set up monitoring and observability — Sentry error tracking, Metabase dashboards, database queries, alerts. Suggests queries and configurations based on the feature or app.
argument-hint: [what to monitor — e.g. "auth failures" or "order processing"]
allowed-tools: Read, Write, Edit, Bash, Grep, Glob
---

# Monitor

Set up monitoring and observability for your feature or application.

## What this skill does

1. **Detects your stack** — Identifies database, backend, and existing monitoring tools
2. **Suggests monitoring points** — Key metrics, errors, and events to track
3. **Generates queries** — SQL for Metabase, Sentry configs, custom dashboards
4. **Sets up alerts** — Thresholds and notification rules

## Supported tools

| Tool | Purpose | What we configure |
|------|---------|-------------------|
| **Sentry** | Error tracking | DSN setup, custom contexts, breadcrumbs, alerts |
| **Metabase** | Analytics dashboards | SQL queries, dashboard configs |
| **Database** | Direct queries | PostgreSQL, MySQL, SQLite monitoring queries |
| **Datadog** | APM & metrics | Tags, custom metrics, monitors |
| **PostHog** | Product analytics | Events, funnels, cohorts |
| **Prometheus** | Metrics | PromQL queries, alerting rules |

## Your task

### 1. Detect the stack

Check for:
```bash
# Package files
cat package.json 2>/dev/null | grep -E "sentry|@sentry|metabase|datadog|posthog"

# Environment files
cat .env .env.example 2>/dev/null | grep -iE "sentry|metabase|datadog|posthog|database"

# Config files
ls *config* 2>/dev/null
ls .github/workflows/*.yml 2>/dev/null
```

Identify:
- **Database:** PostgreSQL, MySQL, SQLite, MongoDB
- **Backend:** Node, Python, Ruby, Go, etc.
- **Existing monitoring:** Sentry, Datadog, etc.
- **Hosting:** Vercel, Railway, AWS, etc.

### 2. Understand what to monitor

Based on user input or recent scope docs, identify:
- **Critical paths** — Auth, payments, core business logic
- **Error-prone areas** — External APIs, file uploads, async jobs
- **Business metrics** — Signups, conversions, retention
- **Performance concerns** — Slow queries, API latency

### 3. Generate monitoring setup

#### Sentry Error Tracking

**Installation:**
```bash
# Node.js
npm install @sentry/node

# Python
pip install sentry-sdk

# React
npm install @sentry/react
```

**Basic setup (Node.js):**
```javascript
import * as Sentry from "@sentry/node";

Sentry.init({
  dsn: process.env.SENTRY_DSN,
  environment: process.env.NODE_ENV,
  tracesSampleRate: 1.0,
});

// Add context to errors
Sentry.setUser({ id: user.id, email: user.email });
Sentry.setTag("feature", "auth");
Sentry.addBreadcrumb({
  category: "auth",
  message: "User attempted login",
  level: "info",
});
```

**Alert rules to create:**
- Error rate > 1% in 5 minutes
- New error type in production
- Specific error patterns (e.g., "payment failed")

#### Metabase / SQL Dashboards

**Common monitoring queries:**

```sql
-- Daily active users
SELECT 
  DATE(created_at) as date,
  COUNT(DISTINCT user_id) as dau
FROM events
WHERE created_at > NOW() - INTERVAL '30 days'
GROUP BY 1
ORDER BY 1;

-- Error rate by endpoint
SELECT 
  endpoint,
  COUNT(*) FILTER (WHERE status >= 400) as errors,
  COUNT(*) as total,
  ROUND(100.0 * COUNT(*) FILTER (WHERE status >= 400) / COUNT(*), 2) as error_rate
FROM api_requests
WHERE created_at > NOW() - INTERVAL '24 hours'
GROUP BY 1
ORDER BY error_rate DESC;

-- Slow queries
SELECT 
  query,
  calls,
  mean_time,
  total_time
FROM pg_stat_statements
ORDER BY mean_time DESC
LIMIT 20;

-- User funnel
WITH funnel AS (
  SELECT 
    COUNT(*) FILTER (WHERE event = 'signup_started') as started,
    COUNT(*) FILTER (WHERE event = 'email_verified') as verified,
    COUNT(*) FILTER (WHERE event = 'first_action') as activated
  FROM events
  WHERE created_at > NOW() - INTERVAL '7 days'
)
SELECT 
  started,
  verified,
  ROUND(100.0 * verified / NULLIF(started, 0), 1) as verify_rate,
  activated,
  ROUND(100.0 * activated / NULLIF(verified, 0), 1) as activation_rate
FROM funnel;
```

#### Database Health Queries

**PostgreSQL:**
```sql
-- Connection count
SELECT count(*) FROM pg_stat_activity;

-- Table sizes
SELECT 
  relname as table,
  pg_size_pretty(pg_total_relation_size(relid)) as size
FROM pg_catalog.pg_statio_user_tables
ORDER BY pg_total_relation_size(relid) DESC
LIMIT 10;

-- Index usage
SELECT 
  relname as table,
  indexrelname as index,
  idx_scan as scans,
  idx_tup_read as tuples_read
FROM pg_stat_user_indexes
ORDER BY idx_scan DESC;

-- Long-running queries
SELECT 
  pid,
  now() - pg_stat_activity.query_start AS duration,
  query
FROM pg_stat_activity
WHERE state != 'idle'
  AND now() - pg_stat_activity.query_start > interval '5 minutes';
```

### 4. Create dashboard config

Output a monitoring plan:

```markdown
## Monitoring Plan: {Feature}

### Metrics to Track
- [ ] {Metric 1} — {why it matters}
- [ ] {Metric 2} — {why it matters}

### Sentry Setup
- DSN configured in .env
- Custom contexts: {list}
- Alert rules: {list}

### Dashboard Queries
1. {Query name} — {what it shows}
2. {Query name} — {what it shows}

### Alerts
| Metric | Threshold | Action |
|--------|-----------|--------|
| Error rate | > 1% | Page on-call |
| Latency p99 | > 2s | Slack alert |
```

### 5. Save and configure

- Save queries to `.claude/output/monitoring/{feature}-queries.sql`
- If Sentry not configured, add setup instructions to scope doc
- If Metabase available, offer to create dashboard via API

## Feature-specific monitoring

### Auth monitoring
- Failed login attempts by user/IP
- Password reset requests
- Session creation/expiry
- OAuth callback errors

### Payment monitoring
- Transaction success/failure rate
- Payment provider errors
- Refund volume
- Revenue by period

### API monitoring
- Requests per endpoint
- Error rate by endpoint
- Latency percentiles
- Rate limit hits

### Background jobs
- Job success/failure rate
- Queue depth over time
- Job duration percentiles
- Stuck/zombie jobs
