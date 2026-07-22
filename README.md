# ai-skills-toolkit

Personal [Claude Code](https://claude.com/claude-code) skills, packaged as a plugin so they install and update the same way on every machine.

This repo is both a plugin marketplace and the plugin itself — there's nothing to build or release. Every commit to `main` is the latest version; there's no version number to bump.

## Install

```
/plugin marketplace add dallinwood/ai-skills-toolkit
/plugin install ai-skills-toolkit@ai-skills-toolkit
```

(Or the equivalent `claude plugin marketplace add` / `claude plugin install` commands from a shell.)

## Update

```
/plugin marketplace update ai-skills-toolkit
/plugin update ai-skills-toolkit@ai-skills-toolkit
```

Claude Code also refreshes marketplaces in the background on startup, so installs generally stay current on their own.

## Adding a skill

Drop a new directory under [skills/](skills/) — see [skills/README.md](skills/README.md) for the layout. Subagents go under `agents/`, auto-discovered the same way. Commit and push; every installed device picks it up on the next update.

## Official Anthropic plugins

`/ai-skills-toolkit:install-official-plugins` installs the official `claude-plugins-official` plugins this setup depends on ([skills/install-official-plugins/SKILL.md](skills/install-official-plugins/SKILL.md)). It's set to manual-invocation only, so Claude won't run it on its own — running it won't touch anything you haven't asked for. To onboard a new official plugin, add its name to the list in that file and re-run the skill.

## Global CLAUDE.md

[skills/sync-claude-md/CLAUDE.md](skills/sync-claude-md/CLAUDE.md) is the tracked, canonical copy of the global `~/.claude/CLAUDE.md`. Run `/ai-skills-toolkit:sync-claude-md` on any machine to pull the latest tracked copy down onto that machine ([skills/sync-claude-md/SKILL.md](skills/sync-claude-md/SKILL.md)) — it updates the plugin first, diffs against the local file, and asks before overwriting anything. It's set to manual-invocation only, so Claude won't run it on its own.

That skill only pulls. To publish a change: edit `skills/sync-claude-md/CLAUDE.md` in a git checkout of this repo, commit, and push — then run the sync skill on every other machine.
