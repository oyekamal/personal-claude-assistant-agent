# Morning Standup Skill

A custom skill that runs at session start to give you a daily status snapshot.

## What It Does

1. **Reads your memory** — User profile, current projects, feedback patterns
2. **Checks Gmail** — Fetches last 24h emails, extracts summaries
3. **Shows status snapshot** — What you're working on, what's urgent
4. **Updates contacts** — Adds new email senders to contacts
5. **Flags actions** — Emails needing reply or decision

## How to Use

```
/morning-standup
```

Your assistant will:
- Load your memory files
- Fetch emails from last 24 hours
- Display a status snapshot
- Suggest actions and replies

## Example Output

```
# Daily Standup — 2026-04-09

## Your Focus
- Training LMS backend (Django)
- React CMS frontend
- Team management

## Recent Emails (last 24h)
1. Anam Masood — "Training module architecture" → ACTION: Reply
2. Manager — "Q2 planning" → INFO: Read for context
3. Team — "Deployment successful" → INFO

## Action Items
- [ ] Reply to Anam about training module
- [ ] Prepare Q2 planning notes
- [ ] Follow up on deployment results

## Upcoming
- Q2 planning session tomorrow
- NIETE integration deadline next week
```

## Installation

1. Save this file to `skills/morning-standup.md`
2. Add to CLAUDE.md auto-start:

```markdown
## Auto-Start Behavior

1. Invoke the `morning-standup` skill — read memory, show daily status snapshot
```

3. Your assistant will run it automatically at session start.

## Customization

Adjust what gets checked:

- **Email frequency** — Change from 24h to 1h or 1 week
- **Email domains** — Filter to work emails only
- **Slack integration** — Add Slack channels to check
- **Jira integration** — Add assigned tickets to summary
- **Calendar** — Show today's meetings

## Example Customized Version

```markdown
# Morning Standup (Customized)

## What It Does

1. Read memory (user profile + projects)
2. Check Gmail for work emails
3. Check Slack #updates and #incidents
4. Show assigned Jira tickets
5. Display calendar for today
6. Flag urgent actions

## Customization

In CLAUDE.md:

```
## Morning Standup Config

- Email: Check last 24h
- Slack: #updates, #incidents only
- Jira: Show assigned issues in MC20
- Calendar: Show all events for today
- Contacts: Update email-tracker.md
```
```

---

This is a foundational skill. Customize it to fit your workflow.
