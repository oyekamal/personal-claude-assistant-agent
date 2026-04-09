# Guide 3: Domains

**Time**: 10 minutes
**Goal**: Organize work into domains

---

## What Are Domains?

Domains are areas of your work or life. Each domain has a folder in `domains/` where you track context, decisions, and history.

**Common domains:**
- `domains/work/` — Your job, projects, career
- `domains/fitness/` — Health, exercise
- `domains/business/` — Side projects
- `domains/content/` — Blog, writing
- `domains/personal/` — Family, growth

---

## Structure of a Domain

```
domains/work/
├── README.md           # Overview
├── work-log.md         # Daily updates
├── projects.md         # Current projects
├── incidents.md        # Problems + solutions
├── contacts/
│   ├── people/
│   │   └── person.md
│   └── email-tracker.md
└── goals.md            # Annual goals
```

---

## Common Files

**README.md**: Overview of the domain, key people, systems

**work-log.md**: Daily tracking
```markdown
# Work Log

## 2026-04-09
- 10:00 — Fixed login bug
- 10:45 — Deployed to staging

## 2026-04-08
- 09:00 — Sprint standup
```

**projects.md**: What you're working on
```markdown
# Projects

## CMS Frontend
- Status: In development
- Deadline: 2026-05-15
- Blockers: None
```

**contacts/email-tracker.md**: Index of people who email you

**incidents.md**: Problems and solutions
```markdown
# Incidents

## S3 Upload Timeout
- Root Cause: Boto3 timeout not configured
- Solution: Added timeout config
- Lesson: [See memory/feedback_s3.md]
```

---

## Creating Your Domains

### Step 1: Identify Domains

What are your main life/work areas? Start with 2-3:

```bash
mkdir -p domains/work
mkdir -p domains/fitness
mkdir -p domains/projects
```

### Step 2: Add Initial Files

```bash
touch domains/work/README.md
touch domains/work/work-log.md
touch domains/work/projects.md
mkdir -p domains/work/contacts/people
```

### Step 3: Populate README

```markdown
# Work Domain

Covers my job at [company], projects, career growth.

## Current Focus
- [Initiative 1]
- [Initiative 2]

## Key People
- Manager: [name]
- Collaborators: [names]

## Key Systems
- Code: GitHub
- Tickets: Jira MC20
```

### Step 4: Start Logging

Append to work-log.md:
```markdown
- HH:MM — [what you did]
```

---

## Best Practices

**Keep domains focused** — One clear purpose each  
**Log consistently** — Update as you work, not end-of-day  
**Archive old projects** — Keep project-archive.md for completed work  
**Link to memory** — Discoveries → memory/feedback_*.md  

---

## Next Steps

- Read [guides/04-workflow-orchestration.md](04-workflow-orchestration.md)
- Check [examples/domains/](../examples/domains/)
