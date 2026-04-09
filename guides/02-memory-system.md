# Guide 2: Memory System

**Time**: 10 minutes
**Goal**: Understand how to build and maintain persistent context across sessions

---

## What Is Memory?

Memory is information your assistant remembers across sessions. It lives in `memory/` and persists in git.

**Memory is NOT:**
- Session chat history
- Recent commits (use `git log`)
- In-progress tasks (use STANDUP.md)
- Debugging solutions (the fix is in code)

**Memory IS:**
- Your profile and preferences
- Validated patterns that worked
- Ongoing project context
- External system references

---

## Four Types of Memory

### 1. User Memory

Who you are, role, expertise, preferences.

**File**: `memory/user_profile.md`

```markdown
---
name: User Profile
description: Senior Backend Engineer, Python/Django
type: user
---

# My Profile

- **Role**: Senior Backend Engineer
- **Expertise**: Python, Django, PostgreSQL, distributed systems
- **Workspace**: Terminal-native, high automation
```

### 2. Feedback Memory

Patterns you've validated. Save corrections and working approaches.

**File**: `memory/feedback_*.md`

```markdown
---
name: Integration Tests
description: Use real database, don't mock
type: feedback
---

# Integration Tests Over Mocks

**Why:** Last quarter, mocked tests passed but prod migration failed.

**How to apply:** Spin up test database for data-layer tests.
```

### 3. Project Memory

Ongoing work, deadlines, blockers, context.

**File**: `memory/projects.md`

```markdown
---
name: Current Projects
description: Projects in flight, deadlines, stakeholders
type: project
---

# Current Projects

**Training LMS Backend**
- Status: Active development
- Deadline: 2026-06-30
- Blockers: NIETE sync reliability
```

### 4. Reference Memory

Pointers to external systems (Jira, Slack, docs).

**File**: `memory/references.md`

```markdown
---
name: Jira Project
description: MC20 on orendatrust.atlassian.net
type: reference
---

# Jira Project MC20

Taleemabad work tracked here. Auto-hook at `hooks/auto-jira.py`.
```

---

## How to Save Memory

### Step 1: Create the file

In `memory/`, create: `user_profile.md`, `feedback_testing.md`, `project_taleemabad.md`, etc.

### Step 2: Add frontmatter

```markdown
---
name: [Name]
description: [One-line hook]
type: [user | feedback | project | reference]
---

[Your content]
```

### Step 3: Update MEMORY.md

```markdown
- [Memory Title](memory/file.md) — one-line description
```

### Step 4: Commit

```bash
git add memory/file.md MEMORY.md
git commit -m "memory: [what this captures]"
```

---

## When NOT to Save Memory

- **Code patterns** — They're in the code
- **Git history** — Use `git log`
- **Debugging solutions** — The fix is canonical
- **Session summaries** — Don't save conversations
- **Ephemeral task lists** — Use STANDUP.md instead

---

## Memory Lifecycle

**Create** → Learn something that shapes future work  
**Use** → At session start, read relevant memories  
**Update** → Discover new information or evolve approach  
**Archive** → When a project finishes or lesson no longer applies  

Every ~3 months, scan memory files. Keep what's useful, retire what's stale.

---

## Next Steps

- Read [guides/03-domains.md](03-domains.md) to organize work by area
- Check [examples/memory/](../examples/memory/) for template files
