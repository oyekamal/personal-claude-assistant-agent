# Guide 1: Initial Setup

**Time**: 5 minutes
**Goal**: Clone scaffold and customize CLAUDE.md for your first session

---

## What You're Setting Up

Your personal Claude assistant workspace has these core pieces:

1. **CLAUDE.md** — Startup behavior, project workflows, logging discipline
2. **STANDUP.md** — Daily carry-overs and session goals
3. **MEMORY.md** — Index of context files
4. **logs/** — Daily session records
5. **memory/** — Persistent context (your profile, feedback, projects)
6. **skills/** — Custom automation (optional)
7. **domains/** — Work area tracking (optional)
8. **plans/** — Planning docs (optional)

---

## Step 1: Copy scaffold/

Clone or copy the scaffold/ folder to your workspace:

```bash
# Option A: Copy to a local workspace
cp -r scaffold ~/my-claude-agent
cd ~/my-claude-agent

# Option B: Fork the repo and clone your fork
git clone https://github.com/YOUR_GITHUB_USERNAME/personal-claude-assistant-agent.git
cd personal-claude-assistant-agent
```

---

## Step 2: Understand CLAUDE.md

Open `CLAUDE.md` (from scaffold/CLAUDE.md.template) and review:

**Auto-Start Behavior** — What happens when you open this workspace in Claude Code
- Email reading
- Memory loading
- Daily standup

**Project-Specific Workflows** — How to define commands for your projects
- Example: `/cms-dev`, `/feature`, etc.
- Shows Taleemabad patterns (concrete) and generic templates

**Workflow Orchestration** — How to approach work
- Plan before implementing
- Use subagents for parallel work
- Verify before marking done

**Task Management** — How to track progress
- TodoWrite patterns
- Marking complete
- Logging lessons

**Logging Discipline** — Writing logs immediately
- Session logs (logs/YYYY-MM-DD.md)
- Commit at end of day
- Never batch logging to end of session

**Error Recovery** — Handling failures
- Blockers
- Escalation
- Context management

---

## Step 3: Customize CLAUDE.md for Your Work

Open `CLAUDE.md` and customize these sections:

### Auto-Start Behavior

Decide what should happen automatically when you start a session. Examples:
- Read Gmail? (yes/no, which email address)
- Run morning standup? (yes/no)
- Update work logs? (yes/no)
- Check Slack? (yes/no)

Keep it simple for now; you can add more later.

### Project-Specific Workflows

Replace the example projects (Taleemabad CMS, Taleemabad Core) with YOUR projects.

**For each project, define:**
- Location (e.g., `~/my-project/`)
- Tech stack (e.g., React + Node.js)
- Type (SPA, API, CLI, etc.)
- Commands (e.g., `/my-dev`, `/my-test`)
- Key features or gotchas

**Example for a Django backend:**

```markdown
### TEMPLATE: Your Django Backend

**Location**: `~/my-project/`
**Tech**: Django + PostgreSQL + DRF
**Type**: REST API

**Commands**:
- `/api-dev` — Run development server
- `/api-test` — Run tests
- `/api-migrate` — Run database migrations

**Key Features**:
- User authentication (JWT)
- REST endpoints
- Async tasks with Celery

**When you're working on this project**: Run tests before committing, check migrations carefully, verify no breaking changes.
```

**Start with 1-2 projects.** You can add more later.

### Workflow Orchestration

Review the 6 principles:
1. **Plan Node Default** — Use plan mode for 3+ step tasks
2. **Subagent Strategy** — Offload parallel work
3. **Self-Improvement Loop** — Update lessons after corrections
4. **Verification Before Done** — Always prove it works
5. **Demand Elegance** — For non-trivial changes, ask "is there a better way?"
6. **Autonomous Bug Fixing** — Don't ask for hand-holding, just fix

These are defaults; you'll customize them as you work.

### Logging Discipline

Key rule: **Write logs immediately, not at end of session.**

Format:
```markdown
# Session Log — YYYY-MM-DD

## Updates
- HH:MM — [what happened]
- HH:MM — [next thing]
```

Create a new log file for each day in `logs/`.

---

## Step 4: Create Your First Memory Files

In the `memory/` directory, create:

**memory/user_profile.md**

```markdown
---
name: My Profile
description: My role and expertise
type: user
---

# My Profile

- **Role**: [Your role: engineer, manager, PM, ops, etc.]
- **Expertise**: [Your main skills]
- **Workspace focus**: [What you're working on]
- **Communication style**: [How you prefer to work]
```

---

## Step 5: Open Claude Code and Start

In the workspace directory:

```bash
claude
```

Claude Code will:
1. Read CLAUDE.md
2. Load your memory files
3. Invoke morning-standup skill (if set up)
4. Show your daily status

Then open STANDUP.md and add:
- Today's focus
- Carry-overs from yesterday (if this is day 2+)
- Known blockers

---

## Next Steps

- Read [guides/02-memory-system.md](02-memory-system.md) to understand persistent context
- Read [guides/04-workflow-orchestration.md](04-workflow-orchestration.md) to learn planning discipline
- Check [examples/](../examples/) for working patterns

---

**Stuck?** See CLAUDE.md "Getting Help" section or check spec.md for comprehensive reference.
