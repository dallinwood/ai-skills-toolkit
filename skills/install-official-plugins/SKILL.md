---
name: install-official-plugins
description: Install (or update) the maintained set of official claude-plugins-official plugins on this machine. Invoke only when the user explicitly asks to install, onboard, or sync the official plugins.
disable-model-invocation: true
allowed-tools: Bash(claude plugin marketplace add:*), Bash(claude plugin marketplace update:*), Bash(claude plugin install:*), Bash(claude plugin list:*)
---

Ensure the following plugins are installed from the `claude-plugins-official` marketplace:

- commit-commands
- skill-creator
- security-guidance
- claude-md-management

(To onboard a new official plugin later, add its name to this list and re-run this skill — nothing else needs to change.)

Do this:

1. Run `claude plugin marketplace add anthropics/claude-plugins-official` (safe to re-run if it's already added).
2. Run `claude plugin list` to see what's already installed.
3. For each plugin in the list above that isn't already installed, run `claude plugin install <name>@claude-plugins-official`. Skip any that are already present.
4. Report which plugins were newly installed and which were already up to date.
