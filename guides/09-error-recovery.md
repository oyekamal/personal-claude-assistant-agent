# Guide 9: Error Recovery

**Time**: 15 minutes
**Goal**: Handle failures, blockers, and escalation gracefully

---

## When Things Fail

Failures happen. How you handle them determines whether you recover quickly or spin in circles.

---

## Failure Categories

### 1. Tool or System Failures

**Test failure** — A test that should pass fails

**Response:**
1. Understand the failure (read the error)
2. Diagnose root cause (not the symptom)
3. If obvious → fix immediately
4. If unclear → debug systematically (check logs, recent changes, environment)

**Don't:** Retry blindly. Understand first.

### 2. Design or Approach Failures

**You realize mid-implementation that the plan was wrong** — Database schema needs rework, API design is flawed, architecture doesn't fit

**Response:**
1. STOP immediately (don't keep pushing)
2. Re-plan the right approach
3. Get approval on new plan
4. Continue with revised plan

**Don't:** Hope it works out. Stop and replan.

### 3. External Blockers

**Waiting on code review** — Can't merge until someone approves  
**Waiting on API** — Backend endpoint not ready yet  
**Waiting on decision** — Need clarification from user  

**Response:**
1. Explicitly flag what you're waiting on
2. Propose alternative work
3. Set follow-up reminder
4. Move on to unblocked work

**Don't:** Sit idle. Find parallel work.

### 4. Resource Limits

**Token limit approaching** (>80% used)  
**Rate limit hit** (API throttling)  
**Context bloat** (main session context too large)  

**Response:**
- **Token limit**: Summarize context, save to memory, dispatch work to subagent
- **Rate limit**: Back off gracefully, batch operations, wait before retrying
- **Context bloat**: Use subagents for exploration; keep main session clean

---

## Communication Cadence

### Long-Running Work (>15 min)

Give brief status update periodically:

```
Investigating X, found Y so far. Continuing...
```

### Waiting for User Input

Be explicit and ask with deadline:

```
Need your input: Should we use JWT or sessions for auth?

Option A: JWT (stateless, works for mobile)
Option B: Sessions (simpler, traditional)

Which direction? Please decide by EOD.
```

### Stuck (>30 min on one thing)

Don't spin. Re-plan or escalate:

```
Spent 30 min debugging S3 timeout issue. Tried:
1. Increased boto3 timeout
2. Checked AWS config
3. Reviewed recent changes

No luck. Escalating to you with full diagnosis:
- Error log shows timeout at [line X]
- Occurs for files >100MB
- Doesn't happen in dev, only prod

Suggest next step: Check AWS CloudWatch logs or contact AWS support.
```

### Nothing Works (>2 attempts)

Escalate with full context:

```
Issue: Login button unresponsive in CMS

Diagnosis:
- Checked browser console → No errors
- Checked network tab → Request hanging
- Checked backend logs → No errors
- Reverted recent changes → Still broken

Questions for you:
- When did this start?
- Did recent deploy change auth logic?
- What's the testing strategy (manual QA, automated)?

Recommend next step: Check recent commits or post-mortem template.
```

---

## Escalation Checklist

When escalating, include:

- [ ] **What I tried** — All attempts made
- [ ] **Root cause** — Best guess at what's wrong
- [ ] **Error logs** — Relevant error messages or stack traces
- [ ] **Questions** — What you need from user
- [ ] **Proposed next steps** — How to move forward

---

## Recovery Patterns

### Pattern: Test Failure Debugging

```
Test fails: "Expected user to be admin, got 'authenticated'"

Diagnosis:
1. Read the test → checks user.is_admin
2. Check implementation → returns user.role == 'admin'
3. Check test data → test user doesn't have admin role set

Fix: Add user.is_admin = True in test setup

Lesson: Ensure test data matches expectations (memory/feedback_testing.md)
```

### Pattern: Git Conflict

```
Merge conflict: Two branches changed same file

Response:
1. Understand both changes (read diffs)
2. Resolve: Which version is correct?
3. Test the merged result (run tests)
4. Commit: Include why you chose each version

Don't: Force push or discard changes without understanding
```

### Pattern: Performance Regression

```
Deploy slows down API by 2x

Response:
1. Identify what changed (git diff main)
2. Profile: Which function is slow? (check logs)
3. Optimize the bottleneck (don't optimize everything)
4. Verify improvement (benchmark before/after)
5. Commit with explanation

Lesson: Profile before optimizing (memory/feedback_performance.md)
```

---

## Error Prevention

### Before Committing

- [ ] All tests pass
- [ ] No breaking changes
- [ ] Code reviewed
- [ ] Performance verified

### Before Deploying

- [ ] Tests pass in CI
- [ ] Migrations run cleanly
- [ ] Rollback plan ready
- [ ] Monitoring set up

### Before Closing Session

- [ ] All changes committed
- [ ] Session logged
- [ ] Blockers documented
- [ ] Carry-overs added to STANDUP.md

---

## Next Steps

- Read [guides/10-evolving-your-template.md](10-evolving-your-template.md) — Customizing workspace
- Review memory files for lessons from past errors
