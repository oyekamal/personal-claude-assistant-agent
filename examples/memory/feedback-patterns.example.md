# Feedback Patterns Example

Template for capturing validated approaches and lessons learned.

---

```markdown
---
name: Integration Tests Over Mocks
description: Use real database in tests, don't mock
type: feedback
---

# Integration Tests Over Mocks

Always use real database in integration tests. Never mock the database layer.

**Why:** Last quarter, mocked tests passed but production migration failed. The mock DB schema diverged from prod, masking the breaking change.

**How to apply:** When writing tests for data-layer code:
1. Spin up a test database (pytest fixture with real DB)
2. Run actual queries
3. Verify behavior against real schema
4. Clean up after each test

**Example:**

```python
@pytest.fixture
def db():
    # Real test database
    return setup_test_db()

def test_user_creation(db):
    # Uses real DB, not mock
    user = User.objects.create(name='John', email='john@example.com')
    assert user.id is not None
    assert User.objects.get(id=user.id).name == 'John'
```

**Avoid:**

```python
# ❌ Don't do this
user_mock = MagicMock()
user_mock.name = 'John'
# Tests pass but prod might fail
```

---

```markdown
---
name: Plan Before Building
description: For 3+ steps or architectural decisions, use plan mode first
type: feedback
---

# Plan Before Building

For any task with 3+ steps or architectural decisions, enter plan mode before writing code.

**Why:** Without planning, I've wasted time on wrong approaches. Planning upfront catches design issues before implementation.

**How to apply:**
1. Describe the feature/task
2. Ask assistant to enter plan mode
3. Review clarifying questions
4. Approve the approach
5. Follow the plan step-by-step

**Never push forward** if something feels wrong mid-implementation. STOP and replan.

**Example situation:**
```
Task: "Add user authentication"
Wrong approach: Write code immediately
Right approach: Plan mode → clarify (JWT vs sessions? Mobile?) → design → implement
```

---

```markdown
---
name: Verify Before Done
description: Never mark task complete without proving it works
type: feedback
---

# Verify Before Done

Never claim a task is complete without proving it works. Use this checklist:

- [ ] **Tests pass** — All tests passing, no skipped tests
- [ ] **No breaking changes** — Existing features still work
- [ ] **Code reviewed** — Verified for style, edge cases
- [ ] **Manual testing** — Tested in UI or manual testing
- [ ] **Regressions checked** — Old features still working

**Why:** Quick shipping of unverified code causes production incidents. Taking 5 min to verify saves hours of debugging later.

**How to apply:**
1. Run full test suite
2. Test manually in app
3. Check git diff for unintended changes
4. Get code review
5. Only then commit and mark done

---

```markdown
---
name: Demand Elegance for Non-Trivial Changes
description: Ask "is there a more elegant way?" for complex implementations
type: feedback
---

# Demand Elegance for Non-Trivial Changes

For non-trivial changes, pause and ask: "Is there a more elegant way?"

**Why:** Hacky solutions accumulate and become technical debt. Taking time to think about elegance prevents future refactoring.

**How to apply:**
1. After writing a non-trivial function, pause
2. Ask: Does this need 5 conditionals or could it use a cleaner pattern?
3. Ask: Is this solving the root cause or patching a symptom?
4. Refactor if there's a better way

**Skip for:** Simple fixes, one-liners, under time pressure

**Example:**

```python
# ❌ Not elegant (5 conditionals for permissions)
if user.role == 'admin':
    can_delete = True
elif user.role == 'moderator' and post.author == user:
    can_delete = True
elif user.role == 'owner':
    can_delete = True
else:
    can_delete = False

# ✅ More elegant (permissions method on model)
class Post(models.Model):
    def user_can_delete(self, user):
        return (user.role == 'admin' or
                user.role == 'moderator' and self.author == user or
                user.role == 'owner')
```

---
```

## How to Use

Create this file as `memory/feedback_[pattern].md` and customize:

1. After learning a pattern or being corrected
2. Include the rule, why, and how to apply
3. Add example code or situation
4. Update quarterly as your understanding evolves

## What to Include

- **Rule** — The pattern or approach to follow
- **Why** — The reason (why does this matter?)
- **How to apply** — When and where to use it
- **Example** — Code snippet or situation demonstrating the pattern
- **What to avoid** — Common mistakes or anti-patterns

## Benefits

When your assistant reads these feedback files:
- Applies lessons automatically (no repeat mistakes)
- Tailors solutions to your preferences
- Recalls context (why you prefer integration tests, not mocks)
- Adapts to your workflow (plan-first approach)

---

Customize these patterns for your team and context.
