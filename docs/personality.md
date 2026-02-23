# Sprint Personality Guide

> "I exist to finish this task."

Sprint's personality is **focused, energetic, and slightly cheeky** — like a helper creature that spawns with one purpose, executes it, and vanishes. Inspired by the Meeseeks philosophy but entirely original.

---

## Core Principles

1. **Personality in the terminal, professionalism in the docs.** The README stays clean. The CLI has flavor.
2. **Fun should help, not distract.** Flavor text is DIM and secondary — never replaces functional output.
3. **Opt-in by default.** Set `flavor: true` in `.agent/config.yml` or `SPRINT_FLAVOR=1` env var.
4. **Original everything.** No copyrighted quotes, characters, or logos. Inspired by, not copied from.

---

## Voice & Tone

| Trait | Example |
|-------|---------|
| Direct | "One task. Let's go." |
| Confident | "Objective acquired." |
| Brief | "Done." |
| Slightly warm | "Nice." |
| Never cute | ~~"Yay! Great job! 🎉"~~ |
| Never sarcastic | ~~"Oh great, another failure."~~ |

**Think:** a focused coworker who's good at their job and doesn't waste words.

---

## Flavor Text Pack

### `sprint run` — Starting a Task

| # | Message |
|---|---------|
| 1 | Objective acquired. |
| 2 | One task. Let's go. |
| 3 | Clear goal detected. |
| 4 | Spinning up. |
| 5 | Locked in. |
| 6 | Spawned for a purpose. |
| 7 | Target identified. |

### `sprint run` / `sprint done` — Task Complete

| # | Message |
|---|---------|
| 8 | Marked complete. Nice. |
| 9 | Short life. Finished work. |
| 10 | Done and gone. |
| 11 | Progress logged. Next? |
| 12 | Task complete. Exiting with dignity. |
| 13 | Clean finish. |
| 14 | One less thing. |

### `sprint loop` — Starting Loop

| # | Message |
|---|---------|
| 15 | Working the loop. |
| 16 | Continuous mode. No wandering. |
| 17 | Loop engaged. |
| 18 | No breaks until the queue is empty. |

### `sprint loop` — Loop Finished

| # | Message |
|---|---------|
| 19 | Loop finished. Momentum preserved. |
| 20 | Queue cleared. |
| 21 | All objectives met. |
| 22 | Nothing left. Good run. |

### `sprint status`

| # | Message |
|---|---------|
| 23 | Here's where things stand. |
| 24 | Current state of the loop. |

### `sprint skip`

| # | Message |
|---|---------|
| 25 | Skipped. No judgment. |
| 26 | Moved past it. Onward. |

### `sprint retry`

| # | Message |
|---|---------|
| 27 | Going again. |
| 28 | Round two. |

### `sprint preview`

| # | Message |
|---|---------|
| 29 | Dry run. Looking ahead. |
| 30 | Here's what's next. |

### `sprint init`

| # | Message |
|---|---------|
| 31 | New loop initialized. |

### `sprint commit`

| # | Message |
|---|---------|
| 32 | Checkpoint saved. |

### Errors

| # | Context | Message |
|---|---------|---------|
| 33 | No task in progress | No active task. Start with `sprint run`. |
| 34 | Bad command usage | That command needs a target. Give it one job. |
| 35 | Validation failed | Didn't pass the gate. Fix and retry. |
| 36 | Too many failures | Too many misses. Pausing to regroup. |
| 37 | All tasks done | Nothing left. Clean exit. |

---

## Mascot Direction

Sprint doesn't have an official mascot yet, but if/when we make one:

### Best-fit concepts

| Name | Vibe |
|------|------|
| **Sprint Ghost** | Appears, finishes, disappears. Minimal and modern. |
| **Focus Wisp** | A glowing spark of intent. Clean, geometric. |
| **Task Sprite** | Tiny helper creature. Energetic but disciplined. |
| **Loop Imp** | Playful but focused. Runs laps. |

### Visual traits (captures the energy without copying anything)

- Bright, energetic color (electric blue, green spark, warm orange)
- Exaggerated "ready to go" expression
- Simple geometric body (circle, diamond, triangle)
- Stopwatch / bullseye / single-checkbox iconography
- Appears + disappears motif (spawn → finish → poof)
- Small. Never the center of attention.

### What to avoid

- Literal blue humanoid creatures (IP territory)
- Overly cute mascots (undermines trust)
- Complex detailed illustrations (doesn't match CLI simplicity)

---

## Implementation Pattern

Flavor text is shown as **DIM secondary text** below the main functional output:

```
✅ Completed: T5: Add authentication
   Short life. Finished work.          ← DIM flavor, only when flavor=true
```

The primary message is always shown. Flavor is additive, never replacing.

### Config

```yaml
# .agent/config.yml
flavor: true    # Enable terminal personality
```

Or via environment variable:

```bash
export SPRINT_FLAVOR=1
```

### Code pattern

```bash
if [ "$FLAVOR" = true ]; then
  echo -e "${DIM}$(pick_flavor "${FLAVOR_RUN_START[@]}")${NC}"
fi
```

---

## Future Ideas

- **`SPRINT_THEME` flag** for full theme packs (colors, icons, flavor style)
- **Seasonal messages** (holiday-themed, milestone celebrations)
- **Achievement-style messages** after N tasks completed ("10 tasks down. Machine.")
- **Custom flavor packs** — users supply their own message files

---

## Adding New Messages

When adding flavor text:

1. Keep it under 50 characters
2. No exclamation marks (too excited)
3. No questions to the user (it's a statement, not a conversation)
4. Test that it reads well in DIM color against a dark terminal
5. Add it to both this doc and the `FLAVOR_*` array in `src/sprint`
