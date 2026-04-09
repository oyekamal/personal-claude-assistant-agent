# Personal Claude Assistant Agent

A comprehensive template and guide for building your own Claude Code personal assistant—an AI-powered agent that manages your email, tracks contacts, organizes work, and automates your workflow.

## What Is This?

This repo is a **public blueprint** for setting up a Claude Code agent tailored to your work. Whether you're an engineer managing multiple projects, a manager coordinating teams, or a professional handling complex workflows, this template shows you how to structure an AI assistant that works with you.

**This is NOT:**
- A SaaS product or cloud service
- A pre-built tool you can immediately use
- A one-size-fits-all solution

**This IS:**
- A template you customize for your needs
- Patterns proven in production
- A starting point that evolves with your work

## Who Is This For?

- **Engineers** managing multiple codebases, deployments, and teams
- **Managers** tracking projects, people, and blockers
- **Product managers** coordinating sprints and cross-team work
- **Operations** managing incidents, runbooks, and escalations
- **Anyone** with complex, multi-threaded work

## Quick Start

```bash
# 1. Clone or fork this repo
git clone https://github.com/oyekamal/personal-claude-assistant-agent.git
cd personal-claude-assistant-agent

# 2. Copy scaffold/ to your workspace
cp -r scaffold ~/my-claude-agent
cd ~/my-claude-agent

# 3. Read the setup guide
cat ../personal-claude-assistant-agent/guides/01-setup.md
```

Then customize `CLAUDE.md` with your projects, read the relevant guides, and start using your agent.

## What Can It Do?

Your Claude assistant can:
- **Read & summarize email** — Process Gmail, extract action items, track conversations
- **Manage contacts** — Auto-create contact records from email senders
- **Track work** — Daily standups, session logs, project context
- **Orchestrate workflows** — Planning, subagents for parallel work, verification loops
- **Manage tasks** — TodoWrite for progress tracking, nested tasks, priorities
- **Run custom skills** — Automate deployment, testing, reporting, reviews
- **Escalate** — Know when to ask for help, handle blockers gracefully

## Learn More

- **[Getting Started](guides/01-setup.md)** — Initial workspace setup (5 min)
- **[Workflow Orchestration](guides/04-workflow-orchestration.md)** — Planning, subagents, verification (key patterns)
- **[Task Management](guides/05-task-management.md)** — Progress tracking with TodoWrite
- **[Full Reference](spec.md)** — Comprehensive architecture and MCP server setup
- **[Examples](examples/)** — Real Taleemabad patterns + generic templates
- **[All Guides](guides/)** — 10 progressive guides (memory, domains, skills, logging, error recovery, etc.)

## How Guides Are Organized

Read in order or jump to what you need:

| # | Guide | Topic |
|---|-------|-------|
| 1 | [Setup](guides/01-setup.md) | Initial workspace configuration |
| 2 | [Memory System](guides/02-memory-system.md) | Build persistent context (user, feedback, project, reference) |
| 3 | [Domains](guides/03-domains.md) | Organize work by area (work, fitness, projects, etc.) |
| 4 | [Workflow Orchestration](guides/04-workflow-orchestration.md) | Plan-first, subagents, verification, elegance |
| 5 | [Task Management](guides/05-task-management.md) | TodoWrite patterns, progress tracking |
| 6 | [Skills Creation](guides/06-skills-creation.md) | Build custom skills when patterns repeat |
| 7 | [Email Workflow](guides/07-email-workflow.md) | Gmail integration, contact tracking, drafting |
| 8 | [Logging Discipline](guides/08-logging-discipline.md) | Session logs, daily structure, captures |
| 9 | [Error Recovery](guides/09-error-recovery.md) | Handling failures, escalation, blockers |
| 10 | [Evolving Your Template](guides/10-evolving-your-template.md) | Customizing and growing your workspace |

## Real Examples

Learn from working patterns:

- **[Taleemabad CMS](examples/projects/taleemabad-cms.example/)** — Concrete multi-project setup with Jira, S3, deployments
- **[Generic SaaS](examples/projects/generic-saas.example/)** — Template for backend + frontend projects
- **[Generic Backend](examples/projects/generic-backend.example/)** — Template for single backend project

See skills, domain templates, and memory file examples in `examples/`.

## Key Principles

- **Templates evolve** — This is a starting point, not a straitjacket. Remove what doesn't fit, add what you need.
- **Write logs immediately** — Don't batch writing sessions; log as you work.
- **Plan before implementing** — Use plan mode for any non-trivial task.
- **Verify before done** — Prove your work before marking it complete.
- **Simplicity first** — Minimal changes, targeted fixes, no over-engineering.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for how to improve this template or add new guides/examples.

## License

MIT — Use freely, modify, extend.

---

**Ready to start?** Read [01-setup.md](guides/01-setup.md), copy `scaffold/`, and customize for your work.
