# sprint new

Create a new SPRINT.md to start a sprint.

## Usage

```bash
sprint new "Sprint title"
sprint sn "Sprint title"        # Short alias
sprint sprint-new "Sprint title" # Legacy alias
```

## Behavior

1. Checks that no `SPRINT.md` already exists (error if it does)
2. Creates `SPRINT.md` from a template with the given title and today's date

## Generated Template

```markdown
# Sprint title

**Date:** 2025-01-15

## Goal

Describe the sprint goal here.

## Current State

What was just completed? What does the app look like now?

## What We're Building

1. Item one
2. Item two

## What NOT to Do

- Keep scope tight

## Architecture Decisions

Any key decisions for this sprint.
```

Edit the file to fill in the goal, scope, and context before running tasks.

## Examples

```bash
sprint new "Sprint 10: User Auth"
sprint new "API Hardening"
```

## Output

```
✅ Created SPRINT.md — Sprint 10: User Auth
   Edit SPRINT.md to fill in the goal and context.
```

## Errors

| Error | Cause |
|-------|-------|
| `SPRINT.md already exists` | Archive the current sprint first with `sprint archive`. |
| `Usage: sprint new "Sprint title"` | Title argument is required. |

## Typical Workflow

```bash
sprint archive               # Archive previous sprint
sprint new "Sprint 11: Perf" # Create new sprint
vim SPRINT.md                # Fill in goal and context
# Add tasks to TASKS.md
sprint loop                  # Run the sprint
```
