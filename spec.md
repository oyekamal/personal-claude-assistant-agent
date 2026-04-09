# Personal Claude Assistant Agent — Complete Specification

> **Reference material** — This spec covers foundational architecture, MCP server setup, and comprehensive patterns for building personal AI assistants.
>
> **Getting started?** Start with [README.md](README.md) and [guides/01-setup.md](guides/01-setup.md) instead. Return here for reference.

---

## 1. Overview

### What Is a Personal Claude Assistant Agent?

A personal Claude Code agent is an AI-powered assistant that understands your context and automates your workflow. It:

- **Reads your memory** — Persistent context about you, your role, your preferences
- **Manages communications** — Email, Slack, notifications
- **Tracks work** — Logging sessions, maintaining records, follow-ups
- **Orchestrates complex tasks** — Planning, verification, error recovery
- **Learns from feedback** — Captures lessons and improves over time

### Who Is This For?

- **Engineers** — Managing multiple codebases, deployments, team coordination
- **Managers** — Tracking projects, people, blockers, team health
- **Product managers** — Coordinating sprints, feedback, roadmap
- **Operations** — Handling incidents, runbooks, escalations
- **Anyone** with complex, multi-threaded work

### How Does It Work?

You set up a workspace with:
- **CLAUDE.md** — Configuration (projects, commands, startup behavior)
- **Memory/** — Persistent context (your profile, feedback, projects)
- **Logs/** — Session records
- **Domains/** — Work area tracking
- **Skills/** — Custom automation

When you open Claude Code in this workspace, the assistant:
1. Reads CLAUDE.md to understand your setup
2. Loads memory files to understand your context
3. Checks Gmail, Slack, or other systems for updates
4. Shows a daily status snapshot
5. Executes your commands with project-specific context

---

## 2. Architecture

### Workspace Structure

```
my-workspace/
├── CLAUDE.md                    # Startup behavior, projects, workflows
├── STANDUP.md                   # Daily carry-overs, focus
├── MEMORY.md                    # Index of memory files
│
├── logs/                        # Session records (one per day)
│   ├── 2026-04-09.md
│   └── 2026-04-08.md
│
├── memory/                      # Persistent context (persists across sessions)
│   ├── user_profile.md          # Your role, expertise, preferences
│   ├── feedback_*.md            # Validated approaches and lessons
│   ├── project_*.md             # Project context and deadlines
│   └── references.md            # External system references (Jira, Slack, etc.)
│
├── domains/                     # Work area organization
│   ├── work/                    # Job/career
│   │   ├── README.md
│   │   ├── work-log.md
│   │   ├── projects.md
│   │   ├── incidents.md
│   │   └── contacts/
│   │       ├── people/
│   │       └── email-tracker.md
│   ├── fitness/                 # Health, exercise (optional)
│   ├── business/                # Side projects (optional)
│   └── content/                 # Blog, writing (optional)
│
├── plans/                       # Planning documents
│   └── reminders.md             # Explicit reminders to check
│
└── skills/                      # Custom automation (optional)
    ├── morning-standup.md
    ├── deployment.md
    └── ...
```

### Information Flow

```
Session Start
    ↓
Read CLAUDE.md (project setup, workflows)
    ↓
Load memory files (user profile, feedback, projects)
    ↓
Check external systems (Gmail, Slack, etc.)
    ↓
Show status snapshot (what's urgent, what's new)
    ↓
User gives command or starts work
    ↓
Assistant acts with project context
    ↓
Work happens (implementation, email, decisions)
    ↓
Log immediately (YYYY-MM-DD.md)
    ↓
Commit at end of day
    ↓
Update memory if new lessons learned
    ↓
Session end
```

---

## 3. Core Concepts

### Memory (Persistent Context)

Memory persists across sessions. Use it for:

**User Memory** — Your role, expertise, preferences
```markdown
---
name: User Profile
type: user
---

Role: Senior Backend Engineer
Expertise: Python, Django, PostgreSQL
```

**Feedback Memory** — Validated approaches and lessons learned
```markdown
---
name: Integration Tests
type: feedback
---

Always use real DB in tests, not mocks.
Why: Mocks diverged from prod schema last quarter.
```

**Project Memory** — Ongoing work, deadlines, stakeholders
```markdown
---
name: Training LMS
type: project
---

Status: Active development
Deadline: 2026-06-30
Stakeholder: NIETE
```

**Reference Memory** — Pointers to external systems
```markdown
---
name: Jira Project MC20
type: reference
---

Taleemabad tickets tracked here. Auto-hook creates tickets via API.
```

### Domains (Work Organization)

Domains are areas of work/life. Each domain has:
- README (overview)
- work-log.md (daily tracking)
- projects.md (current work)
- contacts/ (email senders)
- incidents.md (problems and solutions)

Common domains:
- work/ — Job, projects, career
- fitness/ — Health, exercise (optional)
- business/ — Side projects (optional)
- content/ — Blog, writing (optional)

### Skills (Custom Automation)

Skills are reusable workflows triggered by commands:
- `/morning-standup` — Daily status snapshot
- `/deploy [staging|prod]` — Deployment workflow
- `/run-tests` — Test validation
- `/debug-api [endpoint]` — API debugging

### Logging (Session Records)

Log immediately as you work, not at end of session:

```markdown
# Session Log — 2026-04-09

## Updates
- 10:15 — Fixed login button styling
- 10:45 — All tests passing (48 tests)
- 11:00 — Replied to Anam's email
- 11:30 — Committed changes
```

Format: `- HH:MM — [what happened]`

---

## 4. Workflow Orchestration

### Principle 1: Plan Before Implementing

For tasks with 3+ steps or architectural decisions → Use plan mode.

```
User: Add user authentication to the API
Assistant: Enters plan mode
  1. Asks clarifying questions (JWT vs sessions? Mobile? Refresh tokens?)
  2. Proposes 2-3 approaches with trade-offs
  3. Designs the solution (schema, endpoints, error handling)
  4. Writes detailed step-by-step tasks
  5. Presents plan for approval
```

If something goes sideways mid-implementation → **STOP and re-plan immediately.** Don't push hoping it works.

### Principle 2: Subagent Strategy

Use subagents for parallel work, research, exploration:

```
User: I need to understand the S3 upload flow
Assistant: Dispatches a research subagent
  - Explores frontend upload component
  - Explores backend presigned URL endpoint
  - Checks S3 CORS configuration
  - Reports findings with key files
```

Benefits:
- Keeps main context clean
- Enables parallel work
- Solves complex problems faster

### Principle 3: Self-Improvement Loop

After corrections, capture lessons in memory:

```
User: "Don't mock the database; use real test DB"
Assistant: Creates memory/feedback_testing.md
  - Rule: Integration tests use real DB
  - Why: Mocks diverged from prod
  - How to apply: When writing data-layer tests
```

Next session, assistant applies the rule automatically.

### Principle 4: Verification Before Done

Never mark tasks complete without proving they work:

- [ ] Tests pass (or justified why not)
- [ ] No breaking changes
- [ ] Code reviewed
- [ ] Manual testing done
- [ ] Regressions checked

### Principle 5: Demand Elegance (Balanced)

For non-trivial changes, ask: "Is there a more elegant way?"

Skip for: Simple fixes, one-liners, under time pressure.

### Principle 6: Autonomous Bug Fixing

When given a bug report, assistant just fixes it:
1. Check error logs
2. Diagnose root cause
3. Find the bug
4. Implement fix
5. Test the fix
6. Verify no regressions
7. Commit

No hand-holding needed.

---

## 5. Task Management

### Planning

Write plan to tasks/todo.md before starting:

```markdown
- [ ] **Task 1: Write failing test**
- [ ] **Task 2: Implement login function**
- [ ] **Task 3: Run tests to verify**
- [ ] **Task 4: Commit**
```

### Tracking

Mark items complete as you work (don't batch at end):

```markdown
- [x] **Task 1: Write failing test** ✓ Done at 10:15
- [x] **Task 2: Implement login function** ✓ Done at 10:30
- [ ] **Task 3: Run tests to verify**
```

### Verification

Before marking done:
- Tests pass
- No breaking changes
- Follows conventions
- Changes minimal

### Documentation

After completing, add review:

```markdown
- [x] **Task 4: Commit**
  - Result: Code committed with message "feat: add login"
  - Tests: All 48 passing
  - Verified: Feature works in UI, no regressions
```

### Lessons

Capture patterns discovered:

```markdown
## Lessons Learned

- Verified: Use integration tests (real DB), not mocks
- Next time: Remember to check edge cases in password reset flow
```

---

## 6. MCP Servers (External Tools)

Model Context Protocol (MCP) servers extend your assistant with tools.

### High-Value Servers

**Google Workspace** — Gmail, Docs, Sheets, Calendar, Contacts
```
- Read emails from Gmail
- Update Google Docs
- Track meetings on Calendar
- Manage contacts
```

**Atlassian** — Jira, Confluence
```
- Create/update Jira tickets
- Search Jira issues
- Read Confluence docs
```

**GitHub** — Pull requests, issues, repositories
```
- Create issues
- Comment on PRs
- Check CI status
- Search repositories
```

**Slack** — Channels, messages, users
```
- Post to channels
- Search messages
- Get user info
```

**Notion** — Databases, pages, documents
```
- Create database entries
- Update pages
- Search content
```

### Situational Servers

**Linear** — Issue tracking (alternative to Jira)  
**Postgres** — Direct database queries  
**Figma** — Design files and exports  
**Airtable** — Spreadsheet databases  
**Stripe/Lemonsqueezy** — Revenue tracking  

### Experimental Servers

**Browser Automation** — Screenshots, navigation  
**Excalidraw** — Diagrams and visuals  
**Langfuse** — LLM observability  

---

## 7. Configuration (CLAUDE.md)

### Auto-Start Behavior

```markdown
## Auto-Start Behavior

At the beginning of every session:

1. Invoke morning-standup skill
2. Read Gmail for [email]
3. Update work logs with email summaries
4. Update contacts with new senders
5. Flag emails needing reply
6. Ask for approval before sending
```

### Project-Specific Workflows

```markdown
## Project-Specific Workflows

### CMS Frontend
Location: repos/taleemabad-cms/
Tech: React + Vite + TypeScript
Commands:
- /cms-dev — Start dev server
- /cms-test — Type-check + lint + build

### Backend API
Location: ~/taleemabad-core/
Tech: Django + PostgreSQL
Commands:
- /api-dev — Start dev server
- /api-test — Run test suite
```

### Workflow Orchestration

Document your approach:

```markdown
## Workflow Orchestration

### Plan Node Default
Enter plan mode for 3+ step tasks or architectural decisions.

### Subagent Strategy
Use subagents for research, exploration, parallel work.

### Self-Improvement Loop
Capture lessons in memory after corrections.

### Verification Before Done
Always prove work before claiming done.
```

### Logging Discipline

```markdown
## Logging Discipline

Write logs immediately (not at end of session).
Format: logs/YYYY-MM-DD.md with HH:MM entries.
Commit at end of day: git commit -m "log: session YYYY-MM-DD"
```

---

## 8. Best Practices

### Logging

- ✅ Log immediately as you work
- ✅ Be specific ("Fixed login button styling")
- ✅ Note blockers and decisions
- ✅ Capture lessons for memory
- ❌ Don't batch logging to end of session

### Memory

- ✅ Save lessons learned
- ✅ Document preferences and patterns
- ✅ Update quarterly
- ✅ Keep memories focused and specific
- ❌ Don't save ephemeral task lists

### Planning

- ✅ Use plan mode for 3+ step tasks
- ✅ Clarify requirements upfront
- ✅ Re-plan if something changes
- ✅ Verify against plan before merging
- ❌ Don't skip planning for "simple" features

### Testing

- ✅ Write tests before implementation (TDD)
- ✅ Use real databases in integration tests
- ✅ Test edge cases and error paths
- ✅ Verify no breaking changes
- ❌ Don't mock databases

### Code Review

- ✅ Review your own code before committing
- ✅ Ask: "Would a staff engineer approve?"
- ✅ Check for edge cases and performance
- ✅ Verify style and conventions
- ❌ Don't commit without reviewing

---

## 9. Error Recovery

### When Things Fail

**Test failure** → Diagnose, don't retry blindly  
**Design issue** → STOP, re-plan, continue  
**External blocker** → Flag what you're waiting on, find parallel work  
**Resource limits** → Summarize, save to memory, delegate to subagent  

### Escalation

When stuck >30 min on one thing:

```
Issue: Login button unresponsive

Diagnosis:
- Checked browser console (no errors)
- Checked network tab (request hanging)
- Checked backend logs (no errors)
- Reverted recent changes (still broken)

Questions:
- When did this start?
- Did recent deploy change auth?

Recommended next step: Check recent commits
```

### Communication Cadence

- **Long research** (>15 min) → Brief status
- **Waiting for input** → Explicit ask with deadline
- **Stuck >30min** → Re-plan or escalate
- **Nothing works** → Full diagnosis + questions

---

## 10. Extending the Template

### Adding Domains

When new work area emerges:

```bash
mkdir -p domains/[new-area]
touch domains/[new-area]/README.md
touch domains/[new-area]/work-log.md
```

### Adding Projects

When managing new project:

Add to CLAUDE.md:

```markdown
### [Project Name]
Location: [path]
Tech: [stack]
Commands: /project-dev, /project-test
```

### Creating Skills

When pattern repeats 2+ times:

```bash
touch skills/[pattern].md

# Structure:
# - What it does
# - How to use
# - Step-by-step workflow
# - Examples
```

### Capturing Lessons

When you learn something:

```bash
touch memory/feedback_[pattern].md

# Structure:
# - Rule/Pattern
# - Why (the reason)
# - How to apply (when/where)
# - Example code or situation
```

---

## 11. Common Patterns

### Authentication (JWT)

Backend generates JWT tokens, frontend stores in localStorage:

```python
# Backend: Generate token
token = jwt.encode({'user_id': user.id}, SECRET_KEY)

# Frontend: Use in requests
headers = {'Authorization': f'Bearer {token}'}
```

### S3 Upload (Presigned URLs)

Backend generates temporary S3 credentials, browser uploads directly:

```python
# Backend: Generate presigned URL
url = s3.generate_presigned_url('put_object', ...)

# Frontend: Upload to S3
fetch(url, {method: 'PUT', body: file})
```

### Async Tasks (Celery)

Long-running work → Background jobs:

```python
# Define task
@shared_task
def send_email(user_id):
    # Long operation

# Trigger asynchronously
send_email.delay(user_id)
```

### Database Migrations

Schema changes → Tracked migrations:

```bash
python manage.py makemigrations
python manage.py migrate

# Commit migration file
git commit -m "migration: add new field"
```

### Testing Patterns

TDD workflow:

```python
# 1. Write failing test
def test_login():
    assert login('user', 'pass') is not None

# 2. Implement minimal code to pass test
def login(username, password):
    return User.objects.get(username=username)

# 3. Run tests to verify
pytest

# 4. Refactor and optimize
def login(username, password):
    user = User.objects.get(username=username)
    if user.check_password(password):
        return user
    return None
```

---

## 12. FAQ

**Q: Can I customize the template?**  
A: Yes! Copy scaffold/, customize immediately for your needs.

**Q: Do I need all the features?**  
A: No. Start minimal, add as you need.

**Q: How often should I update memory?**  
A: When you learn something worth remembering. Every session or weekly, not constantly.

**Q: What if the assistant makes mistakes?**  
A: Correct it, save the lesson to memory, assistant learns.

**Q: Can I use this for team work?**  
A: Yes, but CLAUDE.md is personal. Each team member has their own.

**Q: Is this for non-engineers?**  
A: Yes! Managers, PMs, ops teams all benefit.

**Q: How do I set up Gmail integration?**  
A: Enable Google Workspace MCP server in settings.json.

**Q: Can I use other MCP servers?**  
A: Yes. Configure in settings.json.

---

## 13. Resources

- **Personal Agent Workspace** — https://github.com/Orenda-Project/personal-agent-workspace
- **Claude Code Docs** — https://claude.com/claude-code
- **MCP Servers** — https://modelcontextprotocol.io/servers
- **Getting Help** — See README.md for guides and examples

---

## 14. License

MIT License. Use freely, modify, extend.

---

**Ready to build your agent?** Start with [README.md](README.md) and [guides/01-setup.md](guides/01-setup.md).
