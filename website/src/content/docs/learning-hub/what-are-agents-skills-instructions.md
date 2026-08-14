---
title: 'What are Agents, Skills, Instructions, Hooks, and Plugins'
description: 'Understand the primary customization primitives that extend GitHub Copilot for specific workflows.'
authors:
  - GitHub Copilot Learning Hub Team
lastUpdated: 2026-08-14
estimatedReadingTime: '10 minutes'
prev: false
relatedArticles:
  - ./automating-with-hooks.md
  - ./installing-and-using-plugins.md
  - ./agentic-workflows.md
  - ./agents-and-subagents.md
---

Building great experiences with GitHub Copilot starts with understanding the core primitives that shape how Copilot behaves in different contexts. This article clarifies what each artifact does, how it is packaged inside this repository, and when to use it.

## Agents

Agents are configuration files (`*.agent.md`) that describe:

- The tasks they specialize in (for example, "Terraform Expert" or "LaunchDarkly Flag Manager").
- Which tools or MCP servers they can invoke.
- Optional instructions that guide the conversation style or guardrails.

When you assign an issue to Copilot or open the **Agents** panel in VS Code, these configurations let you swap in a specialized assistant. Each agent in this repo lives under `agents/` and includes metadata about the tools it depends on.

In products that support delegation, a primary agent can also launch temporary subagents for focused work such as planning, research, or review. See [Agents and Subagents](../agents-and-subagents/) for the coordination model.

### When to reach for an agent

- You have a recurring workflow that benefits from deep tooling integrations.
- You want Copilot to proactively execute commands or fetch context via MCP.
- You need persona-level guardrails that persist throughout a coding session.
- You want a coordinator that can delegate narrower work to subagents.

## Skills

Skills are self-contained folders that package reusable capabilities for GitHub Copilot. Each skill lives in its own directory and contains a `SKILL.md` file along with optional bundled assets such as reference documents, templates, and scripts.

A `SKILL.md` defines:

- A **name** (used as a `/command` in VS Code Chat and for agent discovery).
- A **description** that tells agents and users when the skill is relevant.
- Detailed instructions for how the skill should be executed.
- References to any bundled assets the skill needs.

Skills follow the open [Agent Skills specification](https://agentskills.io/home), making them portable across coding agent systems beyond GitHub Copilot.

### Why skills over prompts

Skills replace the earlier prompt file (`*.prompt.md`) pattern and offer several advantages:

- **Agent discovery**: Skills include extended frontmatter that lets agents find and invoke them automatically—prompts could only be triggered manually via a slash command.
- **Richer context**: Skills can bundle reference files, scripts, templates, and other assets alongside their instructions, giving the AI much more to work with.
- **Cross-platform portability**: The Agent Skills specification is supported across multiple coding agent systems, so your investment travels with you.
- **Slash command support**: Like prompts, skills can still be invoked via `/command` in VS Code Chat.

### When to reach for a skill

- You want to standardize how Copilot responds to a recurring task.
- You need bundled resources (templates, schemas, scripts) to complete the task.
- You want agents to discover and invoke the capability automatically.
- You prefer to drive the conversation, but with guardrails and rich context.

## Hooks

Hooks are shell scripts that run automatically at key lifecycle events during a Copilot agent session—when a session starts or ends, when a prompt is submitted, or before and after the agent uses a tool. Unlike instructions or skills, hooks are **deterministic and AI-independent**: they execute outside the model and can block actions (for example, preventing a commit that fails linting).

Hooks live under `hooks/` in this repository, each in its own folder containing a `hooks.json` configuration and optional bundled scripts.

### When to reach for a hook

- You want to enforce formatting, linting, or security checks automatically.
- You need a guardrail that must run every time—regardless of whether the AI remembers.
- You want to intercept or enrich prompts before the model processes them.
- You want to log or audit agent activity.

See [Automating with Hooks](../automating-with-hooks/) for configuration details and examples.

## Plugins

Plugins are installable packages that bundle agents, skills, hooks, and MCP server configurations into a single unit you can install with one command. Instead of manually copying files and configuring servers across projects, plugins let you share a complete, versioned set of capabilities with your team or the community.

Plugins are distributed through the GitHub Copilot CLI marketplace and can be installed with:

```bash
copilot plugin install <plugin-name>
```

### When to reach for a plugin

- You want to distribute a curated set of agents, skills, and hooks as one unit.
- You want to share a capability with your team or contribute to the community.
- You need a self-contained toolkit that includes MCP server configuration.

See [Installing and Using Plugins](../installing-and-using-plugins/) for installation and management instructions.

## Instructions

Instructions (`*.instructions.md`) provide background context that Copilot reads whenever it works on matching files. They often contain:

- Coding standards or style guides (naming conventions, testing strategy).
- Framework-specific hints (Angular best practices, .NET analyzers to suppress).
- Repository-specific rules ("never commit secrets", "feature flags must live in `flags/`").

Instructions sit under `instructions/` and can be scoped globally, per language, or per directory using glob patterns. They help Copilot align with your engineering playbook automatically.

### When to reach for instructions

- You need persistent guidance that applies across many sessions.
- You are codifying architecture decisions or compliance requirements.
- You want Copilot to understand patterns without manually pasting context.

## How the artifacts work together

Think of these artifacts as complementary layers:

1. **Instructions** lay the groundwork with long-lived guardrails.
2. **Skills** let you trigger rich, reusable workflows on demand—and let agents discover those workflows automatically.
3. **Agents** bring the most opinionated behavior, bundling tools and instructions into a single persona.
4. **Hooks** enforce deterministic guardrails at lifecycle boundaries, independent of the AI.
5. **Plugins** bundle all of the above into shareable, installable packages.
6. **Agentic Workflows** automate multi-step tasks by running agents in GitHub Actions on schedules, events, or slash commands.

By combining these primitives, teams can achieve:

- Consistent onboarding for new developers.
- Repeatable operations tasks with reduced context switching.
- Tailored experiences for specialized domains (security, infrastructure, data science, etc.).
- Automated enforcement of standards that doesn't rely on the AI remembering the rules.

## Next steps

- Explore the rest of the **Fundamentals** track for deeper dives on chat modes, collections, and MCP servers.
- Browse the [Awesome Agents](../../agents/), [Skills](../../skills/), and [Instructions](../../instructions/) directories for inspiration.
- Learn how to automate lifecycle events with [Hooks](../automating-with-hooks/) and distribute your work as [Plugins](../installing-and-using-plugins/).
- Automate GitHub repository tasks with [Agentic Workflows](../agentic-workflows/).
- Try generating your own artifacts, then add them to the repo to keep the Learning Hub evolving.

---
