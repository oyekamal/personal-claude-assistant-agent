# Guide 5: Task Management

**Time**: 10 minutes
**Goal**: Track progress and mark tasks complete effectively

---

## Task Management Pattern

### 1. Plan First

Before starting work, write the plan. Use TodoWrite to create tasks:

```
- [ ] **Step 1: Write failing test**
- [ ] **Step 2: Run test to verify it fails**
- [ ] **Step 3: Implement minimal code**
- [ ] **Step 4: Run test to verify it passes**
- [ ] **Step 5: Commit the code**
```

Save plan to `tasks/todo.md` or reference in STANDUP.md.

### 2. Track Progress

Mark items complete as you work. Don't batch updates at the end.

```
- [x] **Step 1: Write failing test** — Done at 10:15
- [x] **Step 2: Run test to verify it fails** — Done at 10:20
- [ ] **Step 3: Implement minimal code** — Working on this
- [ ] **Step 4: Run test to verify it passes**
- [ ] **Step 5: Commit the code**
```

### 3. Verify Before Done

Before marking a task complete, verify:

- [ ] Tests pass (if applicable)
- [ ] No breaking changes
- [ ] Code follows project conventions
- [ ] Changes only touch what's necessary

### 4. Document Results

After completing, add a review section:

```
- [x] **Step 5: Commit the code**
  - Result: Code committed with message "feat: add feature"
  - Tests: All 42 tests passing
  - Verified: Feature works in UI, no regressions
```

### 5. Capture Lessons

After corrections or discoveries, update memory:

```
# Session Result

## What Got Done
- Implemented authentication feature (5 tasks)
- All tests passing
- Deployed to staging

## What Carries Over
- Code review from Anam pending

## Lessons Learned
- [See memory/feedback_testing.md] — Use integration tests, not mocks
```

---

## Task Granularity

Each task should be 2-5 minutes of work:

**Too broad:**
- "Implement authentication system"

**Better:**
- "Write the failing test for login endpoint"
- "Run test to verify it fails"
- "Implement minimal login function"
- "Run test to verify it passes"
- "Commit the code"

---

## Using TodoWrite

Claude Code has a TodoWrite tool for task management. Your assistant can create tasks for you:

```
I want to refactor the user model. Please create a task list.
```

Your assistant creates:

```markdown
- [ ] **Task 1: [description]**
- [ ] **Task 2: [description]**
- [ ] **Task 3: [description]**
```

You complete them one by one, marking as you go.

---

## End of Session

**Summary what got done:**
```markdown
## Session Summary (2026-04-09)

**Completed:**
- ✅ Feature: User authentication
- ✅ Tests: All 42 passing
- ✅ Deployed: To staging

**Carries Over:**
- [ ] Code review from Anam
- [ ] Performance testing

**Commit:**
```bash
git add -A && git commit -m "feat: user authentication + tests"
```

---

## Next Steps

- Read [guides/08-logging-discipline.md](08-logging-discipline.md) — Session logging
- Check [guides/10-evolving-your-template.md](10-evolving-your-template.md) — Growing your workspace
