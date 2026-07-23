---
name: sync-claude-md
description: Pull this plugin's tracked CLAUDE.md down onto this machine's global ~/.claude/CLAUDE.md. Invoke only when the user explicitly asks to sync, pull, or update their global CLAUDE.md from this plugin.
disable-model-invocation: true
allowed-tools: Bash(claude plugin marketplace update:*), Bash(claude plugin update:*)
---

This skill tracks a canonical copy of the user's global CLAUDE.md at `${CLAUDE_PLUGIN_ROOT}/skills/sync-claude-md/CLAUDE.md` (right alongside this file). `${CLAUDE_PLUGIN_ROOT}` is the root of this whole plugin repo, not this skill's own folder — so don't shorten this to `${CLAUDE_PLUGIN_ROOT}/CLAUDE.md`, that resolves to the *repo's own* project CLAUDE.md (now at `.claude/CLAUDE.md`), a completely different file that governs this codebase, not the user's global preferences. The live file Claude Code actually reads is `~/.claude/CLAUDE.md`. This skill brings the tracked copy down onto this machine.

Do this:

1. Run `claude plugin marketplace update ai-skills-toolkit` then `claude plugin update ai-skills-toolkit@ai-skills-toolkit`, so the tracked copy reflects the latest commit before comparing anything.
2. Read `${CLAUDE_PLUGIN_ROOT}/skills/sync-claude-md/CLAUDE.md` — the tracked copy next to this SKILL.md, not the repo's own project CLAUDE.md — and read `~/.claude/CLAUDE.md` (if it doesn't exist yet, treat it as empty).
3. If they're identical, report that `~/.claude/CLAUDE.md` is already up to date and stop.
4. If they differ, show the user a concise summary of what would change, then ask for confirmation before overwriting `~/.claude/CLAUDE.md` with the tracked copy — this file holds machine-global preferences, so don't overwrite it silently.
5. Remind the user: to publish a *new* change, edit `CLAUDE.md` in a git checkout of this repo (next to this `SKILL.md`) and push — this skill only pulls, it doesn't push.
