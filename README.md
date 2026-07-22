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

Drop a new directory under [skills/](skills/) — see [skills/README.md](skills/README.md) for the layout. Commands go under `commands/`, subagents under `agents/`; both are auto-discovered the same way. Commit and push; every installed device picks it up on the next update.

## Official Anthropic plugins

`/ai-skills-toolkit:install-official-plugins` installs the official `claude-plugins-official` plugins this setup depends on ([commands/install-official-plugins.md](commands/install-official-plugins.md)). It's a deliberate, on-demand command rather than an automatic dependency — running it won't touch anything you haven't asked for. To onboard a new official plugin, add its name to the list in that file and re-run the command.
