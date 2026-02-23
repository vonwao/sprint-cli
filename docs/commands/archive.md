# sprint archive

Archive the current sprint and prepare for the next one.

## Usage

```bash
sprint archive
sprint sd              # Short alias
sprint sprint-done     # Legacy alias
```

## What It Does

1. Copies `SPRINT.md` to `sprints/sprint-NN.md` (auto-numbered)
2. Moves completed tasks from TASKS.md into the archive file
3. Replaces removed tasks with tombstone lines in an `## Archived Tasks` section
4. Records a sprint boundary in `.agent/state.json`
5. Removes `SPRINT.md`
6. Creates a git commit: `chore: archive sprint → sprints/sprint-NN.md`

## Archive Location

Completed sprints are stored in `sprints/`:

```
sprints/
  sprint-01.md
  sprint-02.md
  sprint-03.md
```

Each archive contains the original SPRINT.md content plus a `## Completed Task Details` section with the full task bodies.

## TASKS.md After Archiving

Completed tasks are replaced with one-line tombstones:

```markdown
## Archived Tasks
- T1 ✅ Set up project `abc1234` → sprints/sprint-01.md
- T2 ✅ Add core types `def5678` → sprints/sprint-01.md
```

Empty milestone sections are automatically cleaned up.

## When to Use

- At the end of a sprint, after all planned tasks are done (or skipped)
- Before starting a new sprint with `sprint new`

## Example Workflow

```bash
sprint ss                    # Check sprint progress
sprint archive               # Archive current sprint
sprint new "Sprint 10: Auth" # Start a new sprint
```

## Errors

| Error | Cause |
|-------|-------|
| `No SPRINT.md found` | No active sprint to archive. Nothing to do. |
