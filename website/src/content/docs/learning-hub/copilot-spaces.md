---
title: 'GitHub Copilot Spaces'
description: 'Learn how GitHub Copilot Spaces provide shared, persistent context to help teams work faster with AI by giving Copilot the right background knowledge for every task.'
authors:
  - GitHub Copilot Learning Hub Team
lastUpdated: 2026-08-01
estimatedReadingTime: '7 minutes'
tags:
  - spaces
  - context
  - team
  - fundamentals
relatedArticles:
  - ./understanding-copilot-context.md
  - ./copilot-configuration-basics.md
  - ./using-copilot-coding-agent.md
prerequisites:
  - Basic understanding of GitHub Copilot
  - Copilot Pro+, Business, or Enterprise plan
---

GitHub Copilot Spaces (currently in public preview) let you create persistent, curated context that Copilot can draw on across sessions and teammates. Instead of re-explaining your project's architecture, conventions, and goals every conversation, you capture that knowledge once in a Space and Copilot always has it available.

Think of a Space as a briefing document that stays connected to Copilot: a living context layer that makes every AI interaction smarter from the start.

## What Is a Copilot Space?

A **Space** is a named, shareable knowledge container that holds:

- **Context files**: Architecture docs, README sections, API references, or any background material
- **Instructions**: How Copilot should behave when working within this domain
- **Repository links**: One or more repos the Space applies to

When you or a teammate starts a Copilot session with a Space attached, Copilot enters the conversation already knowing your project's background. You don't have to paste docs, repeat conventions, or explain the tech stack.

```
Without Spaces:
  User → "Here's our API design doc [paste] and coding standards [paste]..."

With Spaces:
  User → "Add a new endpoint for user preferences"
  (Copilot already knows the API design and conventions)
```

## Key Capabilities

### Persistent Context

Spaces persist across sessions. Once you've added your architecture doc or API reference to a Space, every future conversation starts with that context already loaded — no pasting, no repeating.

### Team Sharing

Spaces can be shared across your team. A senior engineer can create a Space with the key architectural decisions, and every team member benefits automatically. This is especially valuable for:

- **Onboarding**: New teammates get Copilot with project context built in
- **Cross-functional work**: Non-developers like PMs or QA engineers get Copilot tailored to your codebase
- **Consistency**: Everyone uses the same conventions and background knowledge

### Domain Specialization

Create different Spaces for different domains:

| Space | Purpose |
|-------|---------|
| `frontend-react` | React patterns, component library docs, design system rules |
| `backend-api` | API design principles, database schema, service architecture |
| `infra-terraform` | Infrastructure patterns, environment configs, security policies |
| `data-pipeline` | ETL conventions, data schemas, pipeline standards |

Each domain gets its own curated context, so Copilot gives relevant answers without noise from unrelated parts of the codebase.

## How to Create a Space

Spaces are created and managed on **GitHub.com** and in the **GitHub Copilot app**.

### From GitHub.com

1. Navigate to **github.com/copilot** and sign in
2. Open the **Spaces** tab
3. Click **New Space** and give it a name
4. Add context by:
   - Uploading documents (Markdown, text, PDF)
   - Linking to repository files or folders
   - Writing instructions directly in the Space editor
5. Optionally connect one or more repositories
6. Share the Space with teammates via your organization settings

### From the Copilot App

1. Open the GitHub Copilot app and go to **Spaces** in the sidebar
2. Click **+** to create a new Space
3. Add files, write instructions, and link repositories
4. Select the Space when starting a new session

## Using Spaces in a Session

Once a Space is created, attach it to a session:

- **In the Copilot app**: Select the Space from the session picker before starting
- **On GitHub.com**: Open Copilot chat and choose your Space from the context panel

When a Space is active, Copilot references its context automatically. You'll see a Space indicator in the chat header confirming which Space is loaded.

### What Copilot Gains from a Space

- **Project background**: Architecture decisions, design patterns, technology choices
- **Coding conventions**: Style rules, naming patterns, antipatterns to avoid
- **Domain knowledge**: Business logic, glossary, data model explanations
- **Custom instructions**: Specific behaviors for this team's workflow

## Spaces vs. Other Context Sources

Spaces complement (not replace) Copilot's other context mechanisms:

| Source | Scope | Best For |
|--------|-------|---------|
| **Spaces** | Team/project-wide, persistent | Background knowledge, docs, architectural context |
| **Instructions files** (`.github/instructions/`) | Repository, per-file-pattern | Coding conventions that apply during editing |
| **Custom agents** (`.agent.md`) | Repository, task-specific | Specialized personas and workflows |
| **Skills** | Task-specific | Step-by-step guidance for repeatable tasks |
| **Conversation context** | Session only | Task-specific details and current work |

Use Spaces for the kind of knowledge you'd put in a project wiki. Use instructions files for standards that should influence every code edit. Use agents for specialized roles.

## Best Practices

### Keep Spaces Focused

A Space with 50 loosely related documents becomes noise. Create focused Spaces for specific domains or team functions. Smaller, curated Spaces work better than large catch-all ones.

### Prioritize Stable Knowledge

Spaces work best for information that doesn't change frequently:
- Architecture decisions
- Core conventions
- Glossaries and domain models
- API reference documentation

Avoid adding frequently-changing content like sprint notes or meeting summaries — these create stale context.

### Write Explicit Instructions

Don't just add docs — add a short **instructions** section telling Copilot how to use them:

```markdown
## Instructions for Copilot

You are helping with our React frontend. Key rules:
- Use TypeScript strictly (no `any`)
- Components go in `src/components/` as `.tsx` files
- Use our design system from `@acme/design-system`, not raw HTML
- Check `docs/api-reference.md` for all available API endpoints before suggesting calls
```

### Share Across Your Team

The value of Spaces compounds with adoption. Share Spaces with your whole team so everyone benefits from the curated context, especially during onboarding.

## Common Questions

**Q: Are Spaces available in VS Code?**

A: Spaces are initially available through GitHub.com and the GitHub Copilot app. VS Code integration is planned as the feature matures out of public preview.

**Q: How much content can a Space hold?**

A: Spaces support a substantial amount of context — aim for concise, high-signal content rather than exhaustive documentation. Overly large Spaces may be truncated when loaded.

**Q: Can I use Spaces with the coding agent?**

A: Yes. When a coding agent session starts within a repository that has a Space attached, the agent loads that Space's context alongside repository instructions and skills.

**Q: Is a Space the same as a repository instruction file?**

A: No. Repository instruction files (`.github/copilot-instructions.md` or `.github/instructions/*.instructions.md`) apply automatically to all Copilot interactions in that repo. Spaces are explicitly selected and are better suited for longer-form background knowledge and cross-team sharing.

## Next Steps

- **Understand Context**: [Understanding Copilot Context](../understanding-copilot-context/) — Learn how Copilot assembles context from multiple sources
- **Configure Your Repo**: [Copilot Configuration Basics](../copilot-configuration-basics/) — Set up instructions, agents, and skills at the repository level
- **Use the Copilot App**: [Getting Started with the GitHub Copilot app](../github-copilot-app/) — Manage Spaces alongside sessions and automations

## Further Reading

- [GitHub Copilot Spaces enters public preview (Changelog, July 2026)](https://github.blog/changelog/2026-07-18-github-copilot-spaces-enters-public-preview/)
- [GitHub Copilot Spaces documentation](https://docs.github.com/en/copilot/using-github-copilot/using-copilot-spaces)

---
