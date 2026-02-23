# sprint add

Add a new task to TASKS.md.

## Usage

```bash
sprint add "Task description"
sprint add "Task description" @claude
sprint add "Task description" @codex --depends T3
sprint a "Task description"              # Short alias
```

## Arguments

| Argument | Description |
|----------|-------------|
| `"description"` | Task title (required, quoted string) |
| `@claude` / `@codex` | Agent assignment (optional, defaults to config) |
| `--depends T<n>` | Dependency on another task (optional) |

## Behavior

1. Reads TASKS.md to find the highest existing task ID
2. Generates the next ID (e.g., T1, T2, T3...)
3. Builds a commit message from the title (`feat: <slugified-title>`)
4. Appends a task block to TASKS.md

## Template Support

If `templates/default.md` exists, `sprint add` uses it as a template with variable substitution:

| Variable | Value |
|----------|-------|
| `{{ID}}` | Generated task ID (e.g., T5) |
| `{{TITLE}}` | Task description |
| `{{AGENT}}` | Assigned agent |
| `{{DEPENDS}}` | Dependency or `(none)` |
| `{{COMMIT}}` | Generated commit message |
| `{{COMMIT_PREFIX}}` | `feat` |
| `{{TITLE_LOWER}}` | Slugified title |

Without a template, the default format is used:

```markdown
### T5: Task description @claude
**Artifacts:**
**Commit:** `feat: task-description`

Describe the task implementation here.
```

## Examples

```bash
# Add a simple task (uses default agent from config)
sprint add "Set up CI pipeline"

# Assign to Claude for complex reasoning
sprint add "Refactor auth module" @claude

# Add with a dependency
sprint add "Write integration tests" @codex --depends T4

# Short alias
sprint a "Fix login bug" @claude
```

## Output

```
✅ Added task: T5: Set up CI pipeline @codex
   Commit: feat: set-up-ci-pipeline
```
