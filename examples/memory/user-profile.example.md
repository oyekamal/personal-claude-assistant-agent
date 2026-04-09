# User Profile Example

Template for capturing your role, expertise, preferences, and work style.

---

```markdown
---
name: User Profile
description: Role, expertise, preferences, work style
type: user
---

# My Profile

## Role & Background

- **Current Role**: Senior Backend Engineer
- **Expertise**: Python, Django, PostgreSQL, distributed systems, microservices
- **Years Experience**: 10+ years in software engineering
- **Technical Depth**: Deep backend, comfortable with DevOps, learning frontend

## Work Style

- **Communication**: Async-first, written over spoken, detailed documentation preferred
- **Timezone**: PKT (UTC+5)
- **Work Hours**: 9am-6pm PKT, flexible for urgent issues
- **Decision Making**: Data-driven, ask clarifying questions before committing
- **Feedback**: Direct and specific, prefer "here's the problem and solution" over vague criticism

## Current Focus

- **Primary**: Training LMS backend (Django + Python)
- **Secondary**: React CMS frontend (learning TypeScript)
- **Tertiary**: Team leadership and mentorship

## Tools & Environment

- **Editor**: VS Code + Claude Code extension
- **Terminal**: zsh, heavy CLI user, minimal GUI
- **Version Control**: Git, GitHub, familiar with CI/CD
- **Databases**: PostgreSQL primary, MySQL secondary, some DynamoDB
- **Cloud**: AWS (S3, EC2, RDS), familiar with infrastructure

## Knowledge & Gaps

- **Know deeply**: Backend architecture, database design, API design, testing
- **Know reasonably**: React/TypeScript, DevOps, cloud infrastructure
- **Learning**: Frontend performance optimization, design systems
- **Avoid**: Overly abstract patterns, speculative architecture

## Preferences

- **Code style**: Simple, explicit, readable over clever
- **Documentation**: Prefer examples to prose, show me the code
- **Testing**: Integration tests > unit tests, real database > mocks
- **Automation**: Automate everything that repeats 2+ times
- **Process**: TDD, planning before coding, verification before merging

## Team Context

- **Team size**: Small (2-4 engineers on core team)
- **Management**: Individual contributor with mentorship responsibilities
- **Stakeholders**: NIETE (education partner), internal team

## Goals This Quarter (Q2 2026)

- ✅ Complete training LMS backend feature set
- [ ] Improve CMS frontend type safety
- [ ] Mentor 1 junior engineer
- [ ] Document deployment procedures
- [ ] 10% improvement in API response time

---
```

## How to Use

Create this file as `memory/user_profile.md` and customize:

1. Replace example values with your actual role/expertise
2. Be specific about preferences (helps assistant tailor responses)
3. Include gaps and learning areas (assistant won't assume expertise)
4. Update quarterly (preferences and focus change)

## What to Include

- **Role & Background** — What you do, how deep is your knowledge
- **Work Style** — How you like to communicate and decide
- **Current Focus** — What matters most right now
- **Tools & Environment** — Your dev setup and tools
- **Knowledge** — What you know well, what you're learning, what to avoid
- **Preferences** — Code style, documentation, testing, automation
- **Team Context** — Who you work with, any constraints
- **Goals** — What you want to accomplish this quarter

## Benefits

When your assistant knows your profile:
- Gives answers in your technical depth (no explaining JavaScript basics if you're a backend engineer)
- Respects your preferences (uses real DB for tests, not mocks)
- Matches your communication style (detailed > vague, examples > prose)
- Aligns with your goals (focuses on what matters)
- Learns from feedback (updates memory when you correct approach)

---

Customize this for your context.
