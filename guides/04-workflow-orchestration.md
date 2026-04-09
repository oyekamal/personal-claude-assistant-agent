# Guide 4: Workflow Orchestration

**Time**: 20 minutes
**Goal**: Master planning, subagents, and verification patterns

---

## What Is Workflow Orchestration?

How you and your assistant tackle multi-step work together. Key patterns:
- **Plan before building** — Design first, code second
- **Use subagents for parallel work** — Keep main context clean
- **Verify before done** — Prove it works
- **Learn from feedback** — Capture patterns in memory
- **Demand elegance** — Ask "is there a better way?"

---

## Principle 1: Plan Before Implementing

**For ANY task with 3+ steps or architectural decisions → Enter plan mode.**

### Why Plan?

- Prevents false starts
- Reduces rework
- Clarifies requirements
- Saves time

### How to Plan

Ask your assistant:

```
I want to add user authentication to the API.
Please use /superpowers:writing-plans to create a detailed plan.
```

Your assistant will:
1. Ask clarifying questions
2. Propose approaches with trade-offs
3. Design the solution
4. Write step-by-step tasks
5. Show the plan for approval

**If something goes sideways → STOP and re-plan immediately.** Don't push hoping it works.

---

## Principle 2: Subagent Strategy

Subagents are fresh Claude instances for parallel work.

### When to Use Subagents

- **Long research** (>15 min) — Dispatch research subagent
- **Parallel work** — Multiple independent tasks
- **Complex problems** — More compute helps
- **Exploratory work** — Understanding code

### How to Use Subagents

```
I need to understand the S3 upload flow.
Use an Explore agent to map:
1. Frontend upload component
2. Backend presigned URL endpoint
3. S3 CORS configuration
4. Error handling

Report back with summary and key files.
```

Your subagent explores independently, reports findings.

---

## Principle 3: Self-Improvement Loop

After ANY correction or discovery, capture the pattern.

### How It Works

1. You correct the assistant ("Don't mock the database")
2. Assistant saves to memory (memory/feedback_testing.md)
3. Assistant captures the rule ("Integration tests use real DB")
4. Explains why ("Mocks diverged from prod last quarter")
5. Next session, assistant applies the rule

### Your Own Rules

Create memory files proactively:

```markdown
---
name: Test All Changed Code
description: Always run full test suite before commit
type: feedback
---

# Test All Changed Code

Run full suite (not just files you changed) before commit.

**Why:** Caught regression in integration tests that file-level tests missed.

**How to apply:** `npm test` or `pytest` before git commit.
```

---

## Principle 4: Verification Before Done

Never mark a task complete without proving it works.

### Verification Checklist

- [ ] **Tests pass** (or justified why not)
- [ ] **No breaking changes** (existing features still work)
- [ ] **Follows conventions** (matches project style)
- [ ] **Minimal changes** (only touches what's necessary)
- [ ] **Logged and committed** (session logged, code committed)

### How to Verify (Feature)

```bash
# 1. Run tests
npm test

# 2. Test manually
npm run dev
# Use feature in UI

# 3. Check regressions
# Does existing functionality still work?

# 4. Review your code
git diff main
# Does diff look right?

# 5. Commit
git commit -m "feat: add feature"
```

### How to Verify (Bug Fix)

```bash
# 1. Reproduce the bug
# Show it's broken in main

# 2. Fix minimally
# Targeted change

# 3. Verify it's fixed
# Show the bug is gone

# 4. Run tests + manual checks
npm test

# 5. Commit
git commit -m "fix: resolve bug"
```

### The Staff Engineer Question

Before done, ask: "Would a staff engineer approve this?"

- Is code clear?
- Are edge cases handled?
- Is it performant?
- Does it follow conventions?
- Any gotchas in commit message?

If not → fix before declaring done.

---

## Principle 5: Demand Elegance (Balanced)

For non-trivial changes, pause and ask: "Is there a more elegant way?"

**This is NOT over-engineering.** It's seeing if a better approach exists, given what you now know.

### When to Demand Elegance

- **Writing utility functions** — Could this be simpler or more reusable?
- **Adding new field to model** — Is there a better schema?
- **Fixing a bug** — Is this a patch or does it fix root cause?
- **Refactoring** — Does new structure solve the actual problem?

### When to Skip Elegance

- **Simple, obvious fixes** — One-liner bug fixes don't need rethinking
- **Trivial changes** — Renaming, adding comment
- **Under time pressure** — Ship the fix, iterate later
- **Uncertain** — Working solution > perfect analysis

### How to Demand Elegance

```
I'm about to add a conditional in 5 places to check user permissions.
Knowing everything I know now, implement the more elegant solution.
```

Your assistant will:
- Propose better approach
- Implement cleanly
- Explain why it's better

---

## Principle 6: Autonomous Bug Fixing

When you report a bug, assistant just fixes it. No hand-holding.

### Process

**You report:**
```
Login button doesn't work in the CMS.
```

**Assistant should:**
1. Check error logs
2. Diagnose the problem
3. Find the bug in code
4. Write minimal fix
5. Test the fix
6. Verify no regressions
7. Commit

**Assistant should NOT ask:**
- "Where should I look?"
- "What should I check?"
- "How do I fix this?"

---

## Real Example: Add User Authentication

**Scope:** 3+ steps (design, implementation, testing)
**Action:** Use plan mode

```
I want to add JWT-based authentication to the Django backend.
Please use /superpowers:writing-plans to create a detailed plan.
```

Assistant enters plan mode:
- Asks: JWT vs sessions? Mobile? Refresh tokens?
- Proposes 2-3 approaches
- Designs API, schema, error handling
- Writes detailed plan with tests + implementation
- Shows plan for approval

You review → approve → assistant executes plan task-by-task.

---

## Next Steps

- Read [guides/05-task-management.md](05-task-management.md) — Progress tracking
- Check [examples/projects/](../examples/projects/) — Real patterns
