# Guide 6: Skills Creation

**Time**: 15 minutes
**Goal**: Build custom skills when patterns repeat

---

## What Are Skills?

Skills are reusable, parameterized tasks that your assistant can execute. Use them to automate recurring workflows.

**Examples:**
- `/morning-standup` — Daily status snapshot
- `/deploy [staging|prod]` — Deployment checklist
- `/run-tests` — Test suite validation
- `/debug-api [endpoint]` — Systematic API debugging

---

## When to Create a Skill

Create a skill when:
- A pattern repeats 2+ times independently
- It saves >10 min per use
- It's not obvious from the code
- It applies to multiple projects or workflows

**Don't create skills for:**
- One-time operations
- Trivial tasks (one-liner commands)
- Things better solved by code

---

## Anatomy of a Skill

Skills have 3 parts:

1. **Name** — `morning-standup`, `deploy`, `debug-api`
2. **Description** — What it does and when to use it
3. **Steps** — Detailed workflow

---

## Example: Morning Standup Skill

**File**: `skills/morning-standup.md`

```markdown
---
name: morning-standup
description: Daily standup - reads memory, shows status snapshot, prepares for session
trigger: session-start
---

# Morning Standup Skill

## Purpose

At start of every session, your assistant:
1. Reads your memory files (user profile, projects, feedback)
2. Checks Gmail for last 24h emails
3. Shows you a status snapshot
4. Updates your contacts
5. Flags emails needing action

## How It Works

### Step 1: Load Memory

Read all memory files in `memory/` and summarize:
- Your role and current focus
- Current projects and deadlines
- Any feedback or patterns to remember

### Step 2: Check Gmail

Fetch emails from last 24 hours. Extract:
- Who emailed you
- Subject and summary
- Anything urgent or needing action

### Step 3: Show Status

Display:
```
# Daily Standup — 2026-04-09

## Your Focus
- [From memory: what you're working on]

## Recent Emails (last 24h)
- [Email 1]: [summary]
- [Email 2]: [summary]

## Action Items
- [ ] [Reply to email 1]
- [ ] [Follow up on email 2]

## Upcoming
- [From memory: deadlines, blockers]
```

### Step 4: Update Contacts

For each email sender not in contacts:
- Create file in `domains/[domain]/contacts/people/[name].md`
- Add to `domains/[domain]/contacts/email-tracker.md`

### Step 5: Flag Actions

For each email needing reply:
- Suggest a response
- Ask for approval before sending
- Log the reply to work-log.md

## When to Run

- Automatically at session start (configured in CLAUDE.md)
- Manually: `/morning-standup`

## Customization

Adjust what gets checked (Gmail, Slack, Jira, etc.)
```

---

## How to Create a Skill

### Step 1: Identify the Pattern

Track when you use the same workflow repeatedly. Example:
- Every time you deploy, you follow the same steps
- Every morning, you do the same standup tasks

### Step 2: Document the Workflow

Write down all the steps, including edge cases and error handling.

### Step 3: Create the Skill File

```markdown
---
name: deploy
description: Systematic deployment to staging or prod
---

# Deploy Skill

## Purpose
Automate deployment workflow with verification.

## How It Works

### Step 1: Verify tests pass
### Step 2: Run build
### Step 3: Create backup
### Step 4: Deploy to environment
### Step 5: Run smoke tests
### Step 6: Verify logs
```

### Step 4: Invoke via Skill Tool

When you need the skill:

```
Use /deploy staging
```

Your assistant follows the skill steps.

---

## Skill Best Practices

**Keep skills focused** — One workflow per skill  
**Make them repeatable** — Include all edge cases  
**Document well** — Someone else should understand it  
**Evolve over time** — Update after each use  
**Don't over-design** — Simple skills work best  

---

## Next Steps

- Read [guides/07-email-workflow.md](07-email-workflow.md) — Gmail integration
- Check [examples/skills/](../examples/skills/) — Example skill templates
