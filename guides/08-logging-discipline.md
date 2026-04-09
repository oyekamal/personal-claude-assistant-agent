# Guide 8: Logging Discipline

**Time**: 10 minutes
**Goal**: Write logs immediately, maintain session history

---

## Core Rule

**Write logs immediately, not at the end of the session.**

This is non-negotiable. If you skip logging mid-session, the session becomes unrecoverable.

---

## Why Log Immediately?

- **Captures context** while fresh
- **Prevents lost information** (you remember details NOW, not at 5pm)
- **Enables recovery** (if session gets interrupted, you know what happened)
- **Builds accountability** (what did you actually do?)
- **Creates audit trail** for projects and work

---

## Session Log Format

Create `logs/YYYY-MM-DD.md` for each day:

```markdown
# Session Log — 2026-04-09

## Updates

- 10:15 — Fixed login button styling in CMS
- 10:22 — Added validation test, all 42 tests passing
- 10:30 — Deployed to staging, verified working
- 11:00 — Replied to Anam's email about training module
- 11:15 — Reviewed PR from team member, requested changes
```

**Format**: `- HH:MM — [one line: what happened]`

---

## Meaningful Actions to Log

Log these immediately:

- File edited or created in `domains/`, `plans/`, `skills/`, or code repos
- Email drafted or sent
- Decision made or task completed
- Contact file created or updated
- Jira ticket created
- Code written or reviewed
- Deployment or build
- Bug fixed or feature added

---

## Example Session Log

```markdown
# Session Log — 2026-04-09

## Updates

- 09:30 — Reviewed spec for authentication feature
- 09:45 — Entered plan mode, designed API endpoints
- 10:00 — Approved plan, started implementation
- 10:15 — Wrote failing test for login endpoint
- 10:20 — Implemented minimal login function, test passes
- 10:25 — Added error handling tests
- 10:35 — All tests passing (48 tests)
- 10:40 — Code review: verified no breaking changes
- 10:45 — Committed: `feat: add user authentication with JWT`
- 11:00 — Replied to Anam's training module question
- 11:15 — Updated domains/work/contacts/anam-masood.md
- 11:30 — Logged contact in domains/work/contacts/email-tracker.md
- 11:45 — Session complete, all changes committed

## Summary

**What got done:**
- ✅ User authentication feature (planning + implementation + tests)
- ✅ Email reply to Anam
- ✅ Contact tracking updated

**Commits:**
```
feat: add user authentication with JWT
docs: update contact tracking
```

**Carry-overs:**
- [ ] Performance testing for login endpoint
- [ ] Code review feedback from team

**Lessons:**
- Verified `use integration tests, not mocks` (memory/feedback_testing.md)
- Authentication tests are crucial; don't skip
```

---

## End of Session Commit

At end of every working session:

```bash
git add -A
git commit -m "log: session 2026-04-09"
```

This captures:
- All code changes
- All log updates
- All contact/domain updates
- All memory updates

---

## What NOT to Log

- Generic updates ("working on feature X")
- Vague actions ("stuff done")
- Repetitive entries (same action logged 3x)

Instead, be specific:
- "Fixed typo in login button" ✓
- "Changed styling to match design system" ✓
- "Working on feature" ✗

---

## Log Review Patterns

Every few days, review your logs:

```bash
# See last 5 sessions
tail -50 logs/2026-04-*.md

# See what got done this week
grep -h "^-" logs/2026-04-0[1-7].md
```

Use this to:
- Spot patterns (what takes most time?)
- Identify blockers (what's stuck?)
- Celebrate wins (what got shipped?)
- Plan next session (what carries over?)

---

## Logging and Domains

Mirror your logging in both places:

**1. Session log** — `logs/YYYY-MM-DD.md` (global, everything)

**2. Domain log** — `domains/[domain]/work-log.md` (domain-specific)

```markdown
# domains/work/work-log.md

## 2026-04-09
- 10:15 — Fixed login button styling in CMS
- 10:45 — Deployed to staging
- 11:00 — Replied to Anam about training module
```

Domain logs help you see activity in one area of life/work.

---

## Next Steps

- Read [guides/09-error-recovery.md](09-error-recovery.md) — Handling failures
- Check [guides/10-evolving-your-template.md](10-evolving-your-template.md) — Growing your workspace
