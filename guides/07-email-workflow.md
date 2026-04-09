# Guide 7: Email Workflow

**Time**: 15 minutes
**Goal**: Integrate Gmail, track contacts, and manage email efficiently

---

## Email Integration

Your assistant can read Gmail and extract actionable information.

### What It Can Do

**Read emails** — Fetch from last N hours/days, extract subject, sender, body

**Extract action items** — "You need to reply to this", "This is a blocker"

**Track senders** — Create contact file for each sender

**Draft replies** — Suggest a response, wait for approval before sending

**Update logs** — Append to work-log.md with email summary

---

## Auto-Start Email Tasks

In CLAUDE.md, configure:

```markdown
## Auto-Start Behavior

1. Read Gmail for `your.email@example.com`
2. Fetch messages from last 24 hours
3. Update work logs with anything new
4. Update contacts for any new senders
5. Flag emails needing reply or action
6. Ask for approval before sending emails
```

---

## Contact Tracking

Every time someone emails you, your assistant:

1. **Creates a contact file** — `domains/[domain]/contacts/people/[name].md`

```markdown
---
name: Person Name
email: person@example.com
first_contact: 2026-04-09
---

# Person Name

**Email**: person@example.com  
**First Contact**: 2026-04-09  
**Context**: [What did they email about]
**Last Email**: [Date + summary]
```

2. **Updates email tracker** — `domains/[domain]/contacts/email-tracker.md`

```markdown
# Email Tracker

## 2026-04-09

- **Anam Masood** (anam.masood@niete.pk) — Training module implementation question
- **Manager** — Sprint results review

---

## All Contacts

See `contacts/people/` for detailed files.
```

---

## Email Reply Workflow

### Process

1. **Identify emails needing reply**

```
These emails need a response:
1. Anam Masood — "Training module architecture"
2. Manager — "Sprint review feedback"
```

2. **Draft a reply**

```
Subject: Re: Training module architecture

Hi Anam,

Thanks for your question about the training module architecture...
```

3. **Ask for approval**

```
Ready to send? (yes/no/edit)
```

4. **Send the email**

```bash
git add domains/[domain]/work-log.md
# Log shows: "10:30 — Replied to Anam re: Training module"
```

---

## Email Best Practices

**Don't auto-send emails** — Always review and approve first  
**Log all replies** — Add to work-log.md and contacts  
**Update memory** — If email reveals new project/blocker, capture in memory  
**Archive old threads** — Move old email tracker entries to archive  

---

## Gmail Configuration

Set up in CLAUDE.md:

```markdown
## Gmail Integration

**Email address**: your.email@example.com  
**Fetch frequency**: Every session (auto-start)  
**Lookback window**: Last 24 hours  
**Domains to update**: work, business, personal  

**MCP server**: Google Workspace (configured)
```

---

## Slack Integration (Optional)

If you use Slack, add to auto-start:

```markdown
## Slack Integration

**Workspace**: your.slack.com  
**Channels to monitor**:
- #updates
- #incidents
- #team

**Actions**:
- Flag urgent mentions
- Update work-log with important messages
```

---

## Next Steps

- Read [guides/08-logging-discipline.md](08-logging-discipline.md) — Session logging
- Check [examples/domains/contacts/](../examples/domains/) — Contact templates
