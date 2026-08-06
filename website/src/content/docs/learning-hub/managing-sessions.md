---
title: 'Managing Multiple Sessions'
description: 'Learn how to use the Copilot CLI Sessions sidebar to run multiple concurrent conversations, switch between worktrees, and coordinate parallel work.'
authors:
  - GitHub Copilot Learning Hub Team
lastUpdated: 2026-08-06
estimatedReadingTime: '8 minutes'
tags:
  - sessions
  - copilot-cli
  - worktrees
  - parallel-work
relatedArticles:
  - ./agents-and-subagents.md
  - ./github-copilot-app.md
  - ./using-copilot-coding-agent.md
prerequisites:
  - GitHub Copilot CLI installed
  - Familiarity with basic Copilot CLI sessions
---

The Sessions sidebar lets you run multiple independent Copilot CLI conversations at the same time — each with its own context, model, and working directory. You can work on a bug fix in one session while a long-running refactor runs in another, switching between them instantly without losing any context.

This article explains how to enable and use the Sessions sidebar, manage worktrees for true parallel isolation, and use `/new-worktree` to spawn focused branch-scoped sessions.

## Enabling the Sessions sidebar

The Sessions sidebar is available from v1.0.71 and on by default from v1.0.76. Enable it from the CLI's experimental mode if it isn't already showing:

```
/experimental on
```

Or turn the sidebar directly on via settings:

```
/settings sidebar on
```

Once enabled, the sidebar appears as a panel alongside your active conversation. The footer shows the number of active scheduled prompts, and the sidebar indicates each session's status at a glance (idle, working, waiting for input).

## Working with multiple sessions

### Spawning a new session

Press **`n`** in the sidebar to spawn a new session. The new session inherits the current working directory and your default model, but starts with a clean context.

You can also spawn sessions from the command line before launching the CLI:

```bash
# Open a second session in a different directory
copilot --session-name "api-refactor" /path/to/repo
```

### Switching between sessions

- **Arrow keys** (`↑`/`↓`) move the selection in the sidebar
- **Enter** or a **click** switches to the selected session
- **`x` twice** closes the currently selected session (the CLI confirms before closing)

Active sessions are highlighted with an accent color so you always know which one is focused. Hover-to-focus is off by default — use arrow keys or click to switch intentionally.

### Sessions persist across restarts

Session history is saved automatically. When you restart the CLI, your previous sessions are restored to the sidebar. Use **`/resume`** or the sidebar to pick up exactly where you left off. Resume search matches session titles even when whitespace differs.

### Naming sessions

Give sessions descriptive names so the sidebar stays readable:

```
/session-name auth-refactor
```

The name appears in the sidebar and is searchable with `/resume`.

## Running parallel work with worktrees

Worktrees give each session its own branch and working directory, eliminating the risk of conflicting edits between parallel sessions. This is the recommended pattern for substantial parallel work.

### `/worktree` — Start fresh in a new branch

Create a new git worktree and open a new session inside it, leaving your current changes behind:

```
/worktree feature/auth-improvements
```

The CLI:
1. Creates or switches to the specified branch
2. Creates a new worktree directory
3. Transfers your current session to that worktree
4. Leaves uncommitted changes in the original checkout

This keeps each session's work clearly separated on its own branch.

### `/move` — Carry changes into a new worktree

If you've already started making changes and want to continue them on a new branch:

```
/move feature/auth-improvements
```

Unlike `/worktree`, `/move` carries your uncommitted changes into the new worktree before switching, preserving everything you've done so far.

### `/new-worktree` — Branch out without interrupting current work (v1.0.78+)

The `/new-worktree` command creates a new worktree and immediately starts a **new conversation** inside it, without affecting your active session:

```
/new-worktree feature/notification-system
```

This is the fastest way to spin up a parallel work stream. Your current session continues running while the new session picks up in the fresh worktree. Useful for:

- Starting a second task while the first is still generating output
- Exploring a different approach in parallel
- Handing off a subtask while you continue reviewing in the main session

### Choosing between the three commands

| Command | What it does | Use when |
|---------|-------------|----------|
| `/worktree <branch>` | Move current session to a new worktree, leave changes behind | You want a clean start on a new branch |
| `/move <branch>` | Move current session and carry uncommitted changes with you | You want to continue work already started |
| `/new-worktree <branch>` | Spawn a **new** session in a new worktree | You want to run parallel work without interrupting the current session |

## Tips for efficient multi-session workflows

**Keep sessions focused**: Name each session after the task it's doing (`/session-name fix-login-bug`). This makes the sidebar readable and resuming sessions intuitive.

**Use autopilot for long-running tasks**: Set a session to autopilot before switching away. The session continues working independently while you focus elsewhere. Autopilot stays selected after `task_complete` by default — the session waits for the next instruction.

**Monitor scheduled prompts**: The footer shows the count of active scheduled prompts across all sessions. Use `/limits predict` to estimate how many AI credits a session will need.

**Review session costs**: Open `/chronicle` in any session to see usage and cost history. Use `cost-tips` to understand which sessions are consuming the most credits.

**Sidebar hover focus**: By default, hovering does not switch sessions (preventing accidental context loss). Toggle this with `/settings sidebar.hoverFocus on` if you prefer hover-based switching.

## Session exports and history

Export a session's transcript for sharing or archiving:

```
/export
```

Exported sessions preserve angle brackets in inline code and fenced code blocks. Session history is also searchable across restarts with `/resume`.

## Next steps

- [Agents and Subagents](../agents-and-subagents/) — Learn how to delegate work to subagents, which pair well with multi-session workflows
- [GitHub Copilot app](../github-copilot-app/) — The Copilot desktop app offers similar parallel work capabilities through its own multi-agent interface
- [Automating with Hooks](../automating-with-hooks/) — Configure hooks to run automatically at session lifecycle events

---
