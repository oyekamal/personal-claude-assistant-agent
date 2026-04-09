# Guide 10: Evolving Your Template

**Time**: 10 minutes
**Goal**: Customize and grow your workspace as needs change

---

## Core Principle

**This template is a starting point, not a constraint.**

Copy scaffold/, customize immediately, and evolve as your work changes.

---

## Why Templates Need to Evolve

When you clone scaffold/ on day 1, you don't yet know:
- How many projects you'll manage
- Which communication channels matter most
- What domains of work you care about
- Which patterns will actually help you
- How logging should work for your role

**You discover this in the first 2-3 sessions.** Then you customize.

---

## Customization Points

### CLAUDE.md Customization

**Add more projects** — Start with 2, add more as they emerge

**Change auto-start tasks** — Maybe you don't need Gmail checks, but you do need Slack

**Adjust logging format** — Maybe domain logs are overkill; maybe you need more detail

**Customize error recovery** — If you're a manager, escalation looks different than if you're an engineer

**Update core principles** — Add your own rules or priorities

---

### Directory Structure Customization

**Remove unused domains** — If you only care about work, delete fitness/personal/business

**Add new domains** — Create domains/content, domains/health, etc. as needed

**Organize skills** — Create skills/backend, skills/frontend for domain-specific automation

**Archive old projects** — Move completed work to project-archive.md in domains

---

### Memory Customization

**Create domain-specific memories** — Instead of generic memory/projects.md, create memory/project_cms.md, memory/project_backend.md

**Add feedback patterns** — Every time you learn a lesson, save it to memory/feedback_*.md

**Link to external systems** — Add memory/references_jira.md, memory/references_slack.md as you discover important URLs

---

## Common Evolutions

### Week 1: Getting Started

```
domains/work/ only
1 project (CMS)
Basic CLAUDE.md
Email reading only
```

### Week 2: Adding Patterns

```
domains/work/
+ domains/fitness/ (tracking health goals)
2 projects (CMS + Backend)
+ memory/feedback_testing.md (lessons learned)
+ Email replies tracked
```

### Week 3: Scaling Up

```
domains/work/
+ domains/business/ (side project)
domains/fitness/
3 projects (CMS + Backend + Side Project)
+ memory/project_*.md files
+ Custom skill: morning-standup
+ Separate domain logs
```

### Month 2: Refinement

```
domains/work/ (well-organized)
domains/business/ (side projects)
domains/content/ (blog, writing)
4+ projects
Multiple skills (standup, deploy, test)
Rich memory files (user profile + 10+ feedback patterns)
Automated email tracking
```

---

## When to Customize

### Add a New Domain

When a new area of work/life emerges:

```bash
mkdir -p domains/[new-area]
touch domains/[new-area]/README.md
touch domains/[new-area]/work-log.md
```

Then update MEMORY.md and STANDUP.md.

### Add a New Project to CLAUDE.md

When you start managing a new project:

```markdown
### [Project Name]

**Location**: [path]
**Tech**: [stack]
**Type**: [web app, CLI, library, etc.]
**Commands**: `/project-dev`, `/project-test`
**Key Features**: [list]
```

### Create a New Skill

When you notice a pattern repeating 2+ times:

```bash
touch skills/[pattern-name].md

# Example: If you deploy manually 3 times, create /deploy skill
```

### Add Memory Files

When you learn something worth remembering:

```bash
touch memory/feedback_[pattern].md
# Update MEMORY.md
git add memory/ MEMORY.md
git commit -m "memory: [what you learned]"
```

---

## When to Simplify

### Remove Unused Sections

If you never use something, delete it:

- Don't care about fitness? Delete `domains/fitness/`
- Skills not helping? Don't create more
- Unused template files? Remove them

**Rule:** If you haven't used it in 2 weeks, delete it. You can recreate if needed.

### Archive Old Content

Move completed projects to archive:

```markdown
# domains/work/project-archive.md

## ✅ Completed Projects

### Old Project (Q1 2026)
- Dates: 2026-01-01 to 2026-03-31
- Status: Shipped
- Outcome: Learned X, discovered Y
```

### Consolidate Logs

When logs grow large:

```bash
# Archive old logs
mkdir -p logs/archive
mv logs/2026-01-*.md logs/archive/
mv logs/2026-02-*.md logs/archive/
```

---

## Evolution Checklist

Every 2 weeks, review your workspace:

- [ ] **Domains** — Are they still relevant? Add/remove as needed
- [ ] **Projects** — Do they match reality? Update CLAUDE.md
- [ ] **Skills** — Are any unused? Retire or simplify
- [ ] **Memory** — Any new lessons to capture? Any stale memories?
- [ ] **Logs** — Can you archive old ones?
- [ ] **Contacts** — Any to consolidate or remove?
- [ ] **Patterns** — What's working? What isn't?

---

## Real Example: Quarter Evolution

**Q1 Start:**
```
domains/work/ (only domain)
1 project (CMS)
Basic CLAUDE.md
Email reading
```

**Q1 Mid:**
```
domains/work/
+ domains/business/ (started side project)
2 projects (CMS, Side Project)
+ memory/feedback_testing.md
+ Custom /morning-standup skill
```

**Q1 End:**
```
domains/work/ (well-organized, 3 projects)
domains/business/ (active)
domains/fitness/ (New: health goal for Q2)
3 projects actively managed
5+ memory files
3+ skills
Email + Slack integration
```

**Q2 Start (new quarter):**
Review and reset what doesn't fit anymore. Keep what works. Add what's missing.

---

## Guardrails

**Don't:** Create complexity before you need it  
**Do:** Add features when they solve real problems  

**Don't:** Be afraid to delete or simplify  
**Do:** Ruthlessly cut anything unused  

**Don't:** Force your work into the template  
**Do:** Evolve the template to fit your work  

---

## Summary

Your workspace is alive. It changes as you change. Every 2-3 weeks:

1. **Review** what's working
2. **Add** new domains/projects/skills as needed
3. **Remove** anything unused
4. **Refactor** if something feels wrong
5. **Commit** — `git add -A && git commit -m "evolve: Q2 workspace update"`

The template that works for you is the one you customize relentlessly.

---

## Next Steps

- Review your current workspace structure
- Plan your first evolution (week 1-2)
- Check [examples/](../examples/) for advanced patterns
- Read [CLAUDE.md](../scaffold/CLAUDE.md.template) for deep customization

---

**Remember:** A template is only useful if it fits you. Make it yours.
