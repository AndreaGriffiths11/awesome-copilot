---
title: 'Copilot Code Review'
description: 'Learn how GitHub Copilot reviews pull requests, how to choose review effort levels, and how to configure automatic code reviews.'
authors:
  - GitHub Copilot Learning Hub Team
lastUpdated: 2026-08-18
estimatedReadingTime: '8 minutes'
tags:
  - code-review
  - pull-requests
  - automation
  - github
relatedArticles:
  - ./using-copilot-coding-agent.md
  - ./defining-custom-instructions.md
  - ./copilot-configuration-basics.md
prerequisites:
  - A GitHub account with Copilot Pro, Pro+, Business, or Enterprise
  - Basic familiarity with GitHub pull requests
---

GitHub Copilot can review your pull requests, identify issues, and suggest fixes you can apply with a couple of clicks. Unlike a linter that checks for style issues, Copilot code review understands context — it can flag logic bugs, security vulnerabilities, cross-service risks, and code that violates your project's conventions.

This article explains how Copilot code review works, how to control its thoroughness with **review effort levels**, and how to set up automatic reviews.

## How Copilot Code Review Works

When you request a review, Copilot analyzes the changed files in your pull request alongside your repository's context — including custom instructions, skills, and memory — and produces inline comments with explanations and suggested fixes.

**Where you can use it:**

- GitHub.com (web)
- GitHub Mobile
- VS Code
- Visual Studio
- JetBrains IDEs
- Xcode
- Azure DevOps (public preview)

To request a review, open a pull request and add **Copilot** as a reviewer in the Reviewers section, the same way you would request a review from a teammate.

## Review Effort Levels

One of the most impactful settings for Copilot code review is the **effort level**. This controls the depth of analysis and which underlying model is used.

| Effort Level | Speed | Depth | Best For |
|---|---|---|---|
| **Lite** (default) | Fast | Targeted | Routine changes, quick feedback |
| **Balanced** | Slower | Deep | Security-sensitive code, complex logic, cross-service changes |

### Lite

**Lite** is the default effort level. It provides fast, targeted feedback on common issues such as:

- Obvious bugs and logic errors
- Common security vulnerabilities
- Style inconsistencies
- Missing error handling

Use Lite for everyday changes where you want quick, actionable feedback without waiting for a deep analysis.

### Balanced

**Balanced** routes your pull request to a higher-reasoning model that takes more time to analyze complex logic, track cross-service implications, and reason about subtle security issues. Balanced reviews:

- Spot issues that require tracing data across multiple files or services
- Reason about edge cases in complex algorithms
- Identify architectural patterns that could introduce risk
- Use more AI credits than Lite reviews

Use Balanced for:

- Security-sensitive changes (authentication, authorization, encryption)
- Multi-service pull requests with cross-cutting concerns
- Complex business logic where correctness is critical
- Repositories with strict quality standards

### How to Select an Effort Level

You can choose the effort level directly in the pull request, in the **Reviewers** section where Copilot appears. Organization owners and repository administrators can also set a default effort level for automatic reviews.

After a review completes, the pull request overview comment shows which effort level was used.

## Configuring Automatic Reviews

By default, you manually add Copilot as a reviewer on each pull request. You can also configure automatic reviews so Copilot reviews PRs without manual intervention.

**Configuration options:**

- **Individual users** (Pro/Pro+ plans) — Configure Copilot to automatically review all pull requests you open.
- **Repository owners** — Configure Copilot to automatically review all pull requests in a repository.
- **Organization owners** — Configure Copilot to automatically review pull requests across some or all repositories in the organization.

### Automatic review triggers

You can configure the conditions under which automatic reviews fire:

- **Basic**: When a pull request is opened (not as a draft).
- **Review new pushes**: Every time a new commit is pushed to the pull request.
- **Review drafts**: Reviews fire even on draft pull requests.

### Setting the default effort level

Organization owners and repository administrators can set the default review effort level for automatic reviews:

**For an organization**: Go to Organization Settings → Code planning & automation → Copilot → Code review → Review effort level.

**For a repository**: Go to Repository Settings → Code planning & automation → Copilot → Code review → Review effort level.

## Customizing Review Behavior

Copilot code review uses several sources of context to improve its analysis. Understanding how these sources work helps you get better results.

### Custom Instructions

Provide repository-wide or path-specific rules that influence every review:

- **`.github/copilot-instructions.md`** — Repository-wide rules specific to Copilot. Use for coding standards, architecture defaults, and test expectations.
- **Path-specific `*.instructions.md`** — Files under `.github/instructions/` with an `applyTo` field. Use for language-specific guidance or rules that apply only to certain directories.

**Example** (`.github/copilot-instructions.md`):

```markdown
- All API endpoints must include input validation.
- Never store secrets in environment variables; use the Vault client at src/utils/vault.ts.
- All async functions must handle errors explicitly.
```

### AGENTS.md

For rules you want to share across all AI tools and agents (not just Copilot), place them in a root-level `AGENTS.md` file. Copilot code review reads this file automatically.

### Skills

Skills can be configured as review-focused workflows. If you have a `code-review` skill in your repository, Copilot will invoke it during reviews for task-specific analysis beyond what instructions alone provide.

### Copilot Memory (Public Preview)

If you have a Pro, Pro+, or Max plan, you can enable **Copilot Memory** to let Copilot store and reuse facts it learns about your repository. For example, if Copilot notices that a particular module is frequently modified alongside security-sensitive code, it can factor that into future reviews.

Enable Memory in your Copilot settings at github.com.

## Estimated Cost

Copilot code review uses AI credits, which are consumed differently depending on the effort level:

- **Lite reviews** typically cost $0.05–$1.00 USD in AI credits per review run.
- **Balanced reviews** use more AI credits than Lite reviews. The exact amount depends on the size of the pull request and your repository's custom instructions.

Estimates may change as the models that power Copilot evolve. These estimates do not include GitHub Actions minutes.

## Tips for Better Reviews

**Write specific instructions.** Generic instructions like "follow best practices" don't help Copilot as much as specific ones like "validate all user inputs at the API boundary before passing them to service layers."

**Use Balanced for critical paths.** Save Balanced effort level for pull requests touching authentication, payments, or other high-stakes code. Use Lite for routine changes to keep costs reasonable.

**Iterate on custom instructions.** After a few reviews, look at what Copilot keeps catching or missing. Add targeted instructions to improve future reviews.

**Enable automatic reviews for consistency.** Manual review requests are easy to forget. Enable automatic reviews so every pull request gets a Copilot review, even when the author forgets to request one.

## Further Reading

- [About GitHub Copilot code review](https://docs.github.com/copilot/concepts/agents/code-review) — Official documentation with full reference for all options
- [Configure automatic code review](https://docs.github.com/copilot/how-tos/copilot-on-github/set-up-copilot/configure-automatic-review) — Step-by-step setup for automatic reviews
- [Copilot code review: request a review](https://docs.github.com/copilot/how-tos/use-copilot-agents/request-a-code-review/use-code-review) — How to request a review and work with suggestions
- [Defining Custom Instructions](../defining-custom-instructions/) — Create persistent instructions that guide Copilot's behavior

---
