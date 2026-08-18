---
title: 'Using Automations in the GitHub Copilot app'
description: 'A practical guide to getting started with Copilot app automations using templates, iterative refinement, and real-world examples.'
authors:
  - GitHub Copilot Learning Hub Team
lastUpdated: 2026-08-18
estimatedReadingTime: '10 minutes'
tags:
  - copilot-app
  - automations
  - productivity
  - workflows
relatedArticles:
  - ./github-copilot-app.md
  - ./agentic-workflows.md
  - ./using-copilot-coding-agent.md
prerequisites:
  - Access to the GitHub Copilot app
  - A connected repository
---

Automations are one of the fastest ways to make the GitHub Copilot app useful every day. Instead of manually asking Copilot to do the same recurring work, you save the task once and run it on a schedule or on demand.

If you are not sure where to begin, start with templates, adapt one to your workflow, and iterate from real runs.

## Start with templates (then customize)

When you create a new automation in the Copilot app, browse the built-in templates first. They give you a strong starting point for both prompt structure and scope.

Common examples include:

- **Triage incoming issues** (for example, label issues as `bug`, `enhancement`, or `other`)
- **Fix failing tests nightly** (attempt a fix and open a draft pull request)
- **Prepare weekly release notes** (draft and open a pull request on schedule)

Even if none of these are an exact match, templates are the quickest way to avoid a blank-page start.

## Use the work-surface audit trick

A practical way to discover useful automations is to ask Copilot to audit your work surfaces and suggest candidates.

If you have MCP servers configured (for example, WorkIQ for Microsoft 365 or a Slack MCP server), try a prompt like this in a regular chat first:

> If available, use WorkIQ (Teams/Outlook) and a Slack MCP server to review my recent messages and calendar. Identify where I'm missing follow-ups or repeating work, and suggest a short list of useful automations.

This often produces several concrete automation ideas in one pass. Then turn the best one into a saved automation.

## Create your first automation in the app

1. Open **Automations** in the Copilot app sidebar.
2. Click **New automation**.
3. Start from a template or from scratch.
4. Give it a clear name and a specific prompt.
5. Choose when it runs — see [Trigger types](#trigger-types) below.
6. Optionally enable **Run in the cloud** to let the automation run even when your computer is off (see [Cloud automations](#cloud-automations)).
7. Optionally set mode, model, and reasoning effort.
8. Use **Create and run** for the first run so you can immediately inspect output and refine.

If your first version is only 70% right, that is normal. The fastest path is to iterate from a real run.

## Trigger types

Automations support a range of trigger types, from simple schedules to repository events:

| Trigger | Description |
|---|---|
| **Manual** | Run only when you start it explicitly. |
| **Hourly** | Run every hour. |
| **Daily** | Run at one or more specific times each day. |
| **Weekly** | Run on specific days and times each week. |
| **CRON** | Enter a custom CRON expression for precise scheduling (local automations only). |
| **Issue** | Triggered by repository issue events (e.g., issue created, labeled). Add a search query to limit which issues trigger it. |
| **Pull request** | Triggered by PR events (e.g., opened, new commits pushed). Add filters to limit which PRs trigger it. |

You can configure more than one trigger per automation — the automation runs when any of its triggers occur.

**Event-based triggers** (Issue and Pull request) are particularly useful for automating triage, labeling, review assignment, or draft PR creation in response to real repository activity. For example, an automation triggered on `issue created` can automatically label incoming issues, assign them to a milestone, or start a draft fix.

## Cloud automations

Automations can run in two modes:

- **Local** — Run from your local environment. The automation only runs while your computer is on and the app is running.
- **Cloud** — Run in a cloud environment managed by GitHub. The automation runs on its schedule even when your computer is off.

To create a cloud automation, enable **Run in the cloud** when configuring your automation. For cloud automations, use the **Tools** dropdown to select exactly which capabilities Copilot needs — for example, pushing changes, updating labels, or creating pull requests. Scoping tools to the minimum needed is good security practice.

**Prerequisites for cloud automations:**

- The Copilot cloud agent must be enabled for the repository.
- For Copilot Business or Enterprise, an administrator must enable the cloud agent policy.
- The organization must allow both the cloud agent and automations in the repository.

## Example: Awesome Copilot daily PR summary

Here is a real in-app automation used on the `github/awesome-copilot` repository:

| Field | Value |
|---|---|
| **Name** | Awesome Copilot daily PR summary |
| **Interval** | Daily at 09:00 |
| **Mode** | Autopilot |
| **What it does** | Pulls open PRs via `gh api`, filters to updates in the last 24 hours, and returns a concise summary table |

Why this works well:

- It is narrowly scoped (one repo, one reporting goal).
- It has explicit command examples in the prompt.
- It runs on a predictable cadence and produces a format that is easy to review.

This is a strong starter pattern you can copy for issue triage, release prep, review tracking, or team digests.

## Iterate in chat to improve results

After each run, open a chat and refine the automation prompt directly. Typical refinements:

- Tighten scope (for example, only specific labels, teams, or paths)
- Improve output format (table, checklist, short summary)
- Add clear success criteria (what should be included or excluded)

The goal is not a perfect first prompt. The goal is a useful automation that gets better with each run.

## Real-world ideas from the community

Teams are already using recurring automations for practical work such as:

- Daily status updates for initiative-specific issues
- Review and inbox hygiene tasks
- Recurring personal workflow maintenance

Use these as patterns, then tailor them to your own repo, rituals, and communication style.

## Practical guardrails

- Keep prompts explicit and scoped to one outcome.
- Give the automation only the capabilities it needs.
- Avoid secrets in prompts; use repository secrets and variables where needed.
- Prefer review-friendly outputs so it is easy to trust and iterate.

## Next step

Open **Automations**, pick one template, and convert one recurring task you currently do manually into a daily run. That single win usually makes the next automation obvious.
