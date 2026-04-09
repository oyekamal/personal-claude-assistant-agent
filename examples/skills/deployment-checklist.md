# Deployment Checklist Skill

Systematic deployment workflow to production.

## What It Does

1. **Pre-deployment checks** — Tests, build, migrations
2. **Backup** — Database backup before deployment
3. **Deploy** — Push code to production
4. **Verify** — Health checks, smoke tests
5. **Monitor** — Watch logs for errors
6. **Rollback plan** — Ready to revert if needed

## How to Use

```
/deploy staging
/deploy production
```

Your assistant will:
- Run all checks
- Execute deployment
- Verify success
- Watch logs
- Document what happened

## Pre-Deployment Checklist

- [ ] All tests pass (`npm test` or `pytest`)
- [ ] Code reviewed and approved
- [ ] Build succeeds (`npm run build` or `python manage.py collectstatic`)
- [ ] Migrations ready (if database changes)
- [ ] Environment variables configured
- [ ] Monitoring/alerts configured
- [ ] Rollback plan documented

## Deployment Steps

### 1. Verify Tests

```bash
npm test          # Frontend
pytest --cov      # Backend
```

### 2. Create Database Backup

```bash
# Example for PostgreSQL
pg_dump db_name > backup_$(date +%Y%m%d_%H%M%S).sql
```

### 3. Deploy Code

```bash
# Example: Docker push
docker build -t app:v1.2.3 .
docker push registry/app:v1.2.3

# Example: Git push
git push origin main
# CI/CD pipeline deploys automatically
```

### 4. Run Migrations (if needed)

```bash
python manage.py migrate --noinput
```

### 5. Smoke Tests

```bash
# Basic health checks
curl https://app.example.com/health
curl https://app.example.com/api/status

# Key endpoints
curl https://app.example.com/api/v1/users/ -H "Authorization: Bearer $TOKEN"
```

### 6. Monitor Logs

```bash
# Watch application logs for errors
tail -f /var/log/app.log
# or
kubectl logs -f deployment/app --tail=50
```

### 7. Verify Metrics

- **Response time** — Should be <500ms
- **Error rate** — Should be 0%
- **CPU/Memory** — Should be normal
- **Database** — Should be responsive

## Rollback Plan

If something goes wrong:

```bash
# Option 1: Revert to previous version
git revert [commit-hash]
git push origin main

# Option 2: Use backup
psql db_name < backup_YYYYMMDD_HHMMSS.sql

# Option 3: Manual rollback
# Document steps specific to your app
```

## Post-Deployment

```bash
# 1. Verify deployment success
curl https://app.example.com/health → 200 OK

# 2. Check logs for errors
# No ERROR or CRITICAL lines in logs

# 3. Notify team
# Post in Slack: "v1.2.3 deployed to production"

# 4. Document
# Log to domains/work/work-log.md
# - 14:30 — Deployed v1.2.3 to production, all checks pass
```

## Common Issues & Solutions

**Deployment fails** → Check build logs, rollback to previous version

**Tests failing** → Fix failing tests before deploying

**Migrations fail** → Check migration files, rollback database

**Errors in logs** → Check error logs immediately, rollback if critical

---

Customize this for your deployment pipeline and systems.
