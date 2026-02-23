# sprint

> Short loops. Real progress.

**Define tasks. Assign agents. Ship in loops.**

## What is sprint?

**sprint** is a task queue runner for AI coding agents. Define tasks in markdown, assign them to agents like Codex or Claude Code, and run them in short, repeatable loops. No server, no UI — just files and git.

Not a project manager. Not a Jira replacement. Sprint is the loop that sits between your plan and your agents.

## Features

- **Explicit Task Queue** — Define tasks with clear IDs, dependencies, and expected artifacts
- **Multi-Agent Support** — Assign tasks to `@codex` or `@claude` based on their strengths
- **Loop Mode** — Run tasks continuously with `sprint loop`
- **Sprint Lifecycle** — Archive completed sprints, start new ones
- **Git-Native** — State lives in files and git history

## Quick Example

```markdown
# TASKS.md

### T1: Set up project @codex
**Artifacts:** package.json, tsconfig.json
**Commit:** `chore: initialize project`

Create a TypeScript Node.js project with vitest for testing.

### T2: Implement core types @codex
**Depends:** T1
**Artifacts:** src/types/index.ts
**Commit:** `feat: add core types`

Define TypeScript interfaces for Config, Task, and Result.
```

Then run:

```bash
sprint loop  # Run all tasks continuously
```

## Philosophy

sprint sits between fully manual coding and fully autonomous agents:

- **More structured than Ralph** — explicit task IDs, dependencies, agent assignments
- **Less overhead than Jira** — just markdown files, no server, no UI
- **Git as memory** — every task completion is a commit, progress persists in files

## Get Started

```bash
# Install
git clone https://github.com/vonwao/sprint-cli.git ~/.sprint-cli
export PATH="$HOME/.sprint-cli/src:$PATH"

# Use
cd your-project
sprint init
# Create TASKS.md
sprint loop
```

[Read the full guide →](getting-started/introduction.md)
