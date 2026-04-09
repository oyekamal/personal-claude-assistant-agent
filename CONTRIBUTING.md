# Contributing

This repo is a public blueprint for personal Claude Code agents. Contributions help make it better for everyone.

## What to Contribute

We welcome:

- **New guides** — Share lessons learned (e.g., "Guide: Managing remote teams")
- **New examples** — Document your project setup (e.g., "Example: FastAPI backend")
- **New skills** — Automate workflows others might use (e.g., "Skill: Dependency audit")
- **Improvements** — Better explanations, fixes, clarity
- **Bug reports** — Found an error? Tell us

## What NOT to Contribute

Please don't submit:

- Credentials, API keys, secrets
- Personal/sensitive information
- Project-specific code (e.g., your company's CMS)
- Duplicates of existing guides/examples

## How to Contribute

### 1. Fork the Repo

```bash
git clone https://github.com/YOUR_USERNAME/personal-claude-assistant-agent.git
cd personal-claude-assistant-agent
```

### 2. Create a Feature Branch

```bash
git checkout -b feature/my-contribution
```

### 3. Make Changes

- **New guide**: Add to `guides/XX-topic.md` (follow numbering)
- **New example**: Add to `examples/` folder with README
- **New skill**: Add to `examples/skills/` folder
- **Improvements**: Edit existing files directly

### 4. Follow Style

- Use markdown for all documentation
- Include examples and real code
- Be specific; avoid vague explanations
- Explain *why*, not just *what*

### 5. Test Your Changes

- Read your markdown (does it make sense?)
- Check links (do they work?)
- Verify examples (do they compile/run?)

### 6. Commit

```bash
git add .
git commit -m "docs: add [your contribution]"
```

Example commits:
```
docs: add Guide 11 - Managing Remote Teams
docs: add example - Node.js backend template
docs: add skill - daily-standup
docs: clarify workflow orchestration section
```

### 7. Push and Open PR

```bash
git push origin feature/my-contribution
```

Then open a pull request on GitHub with:
- Clear title: "Add Guide 11 - Managing Remote Teams"
- Description: What you're adding and why
- Any context the maintainer should know

---

## Guidelines

### Guides

- **Audience**: Engineers, managers, professionals with complex work
- **Length**: 1,000-2,000 words
- **Structure**: Include examples, step-by-step instructions, common mistakes
- **Testing**: Have you used this pattern? Be specific about results

### Examples

- **Completeness**: Should someone be able to clone this and use it?
- **Documentation**: Include README explaining the setup
- **Realism**: Based on real work, not theoretical
- **Privacy**: Sanitize any sensitive names/URLs

### Skills

- **Focus**: One workflow per skill
- **Clarity**: Someone unfamiliar should understand the steps
- **Automation**: Does this actually save time (>10 min per use)?
- **Testing**: Have you tested the skill?

---

## Code of Conduct

- Be respectful and inclusive
- Give credit where it's due
- Help others learn and grow
- Assume good intent

---

## Questions?

- Open an issue on GitHub
- Discuss in pull request comments
- Check existing guides for context

---

## License

All contributions are submitted under the MIT License. By contributing, you agree that your work can be used and modified by others.

---

**Thank you for making this better for everyone!** 🙌
