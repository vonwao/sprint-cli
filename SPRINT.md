# Sprint 09 — Harden Loop + Fix Agent Integration

**Date:** 2026-02-22
**Principle:** Queue-first. Make the existing system more robust, not more complex.

## Goal

Two themes:
1. **Fix Agent Integration (C):** Replace the fragile CLAUDE.md symlink hack with `--append-system-prompt`. Make both agent paths (codex/claude) consistent.
2. **Harden Loop Mode (A):** Richer progress blocks (duration, files changed), explicit stop reasons, .gitignore hygiene.

## Non-goals

- No rename (Sprint 10)
- No docs updates (Sprint 10)
- No new commands
- No planning mode / agent self-direction

## Acceptance Criteria

1. The CLAUDE.md symlink is gone — AGENT.md injected via `--append-system-prompt` for claude, temp file for codex
2. `.gitignore` exists with sensible defaults (CLAUDE.md, .agent/*.sock, etc.)
3. Progress blocks include duration (seconds) and files-changed count
4. Loop mode records explicit stop reasons in progress blocks
5. `bash -n src/next` passes
6. Backward compatible

## Key Architecture Decision

**Why `--append-system-prompt` instead of prepending to user prompt:**
- AGENT.md is project-level context — it belongs in the system prompt, not mixed with task instructions
- Claude Code natively reads CLAUDE.md as project context; `--append-system-prompt` is the official way to inject equivalent context in `--print` mode
- Keeps the user prompt clean: just guardrails + sprint + task + progress tail
- Codex path stays as-is (temp file prepend) since codex doesn't support system prompts
