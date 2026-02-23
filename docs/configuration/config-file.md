# Config File

Configuration lives in `.agent/config.yml`.

## Options

```yaml
# Default agent if not specified in task header
agent: codex    # codex | claude

# Auto-approve all agent actions
yolo: true      # true | false

# Validation command run before marking a task done
validate: pnpm test --run

# Desktop notifications on task completion/failure
notifications: true

# Fun terminal personality (see personality.md)
flavor: false
```

## Fields

### agent

Default agent for tasks without an `@agent` tag:

```yaml
agent: codex   # Fast, well-defined tasks
agent: claude  # Complex reasoning tasks
```

### yolo

Run agents in fully autonomous mode:

- `true` — No approval prompts (recommended for loop mode)
- `false` — May pause for approvals

### validate

Command to run before marking a task done:

```yaml
validate: pnpm test --run
```

If validation fails, the task stays in progress and the loop pauses. Fix the issue and use `sprint done` or `sprint retry`.

### notifications

Desktop notifications when tasks complete or fail:

```yaml
notifications: true   # Enable (default)
notifications: false  # Disable
```

Uses `osascript` on macOS and `notify-send` on Linux.

### flavor

Enable terminal personality — short flavor text lines shown below functional output:

```yaml
flavor: true    # Enable
flavor: false   # Disable (default)
```

See [Personality](../personality.md) for the full flavor text guide.

## Environment Variable Overrides

Config values can be overridden with environment variables:

| Env Var | Effect |
|---------|--------|
| `SPRINT_FLAVOR=1` | Enable flavor text (overrides `flavor` in config) |

```bash
# One-off flavor mode
SPRINT_FLAVOR=1 sprint loop

# Persistent (add to shell profile)
export SPRINT_FLAVOR=1
```
