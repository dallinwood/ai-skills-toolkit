# ai-skills-toolkit

A single repo that's both a Claude Code plugin marketplace and the plugin itself (`.claude-plugin/marketplace.json` + `.claude-plugin/plugin.json`, plugin source `"./"`). No `version` field anywhere, on purpose — Claude Code falls back to the git commit SHA, so every push is automatically the latest version with no release step to manage.

## Do not touch the live plugin/marketplace config without asking first

`claude plugin marketplace add/install/update/remove` (and the `/plugin ...` slash equivalents) all mutate real, global, shared state under `~/.claude/plugins/` — `known_marketplaces.json`, `installed_plugins.json`, and `~/.claude/settings.json`'s `extraKnownMarketplaces`/`enabledPlugins`. This is the user's actual live Claude Code setup across every project, not repo-scoped test fixtures.

Concretely, this has already gone wrong twice in this repo's history:

- A local-path marketplace test (`claude plugin marketplace add c:/git/ai-skills-toolkit`) reused the marketplace name `ai-skills-toolkit`, silently overwriting the real GitHub-source registration in `known_marketplaces.json` with a local `directory` source, and left a stray `.claude/settings.local.json` in this repo.
- A hand-edit to work around a Windows Defender install bug wrote `known_marketplaces.json` directly but missed the matching `extraKnownMarketplaces` entry in `~/.claude/settings.json`, leaving the two out of sync.

**Rule: don't run any command that adds, installs, updates, or removes a marketplace/plugin — and don't hand-edit the files under `~/.claude/plugins/` or `~/.claude/settings.json` — without explicit, per-action approval from the user first.** This applies even for "just testing" a change to this repo; it is not sandboxed, it's the user's real setup.

- Prefer `claude plugin validate .` for checking `marketplace.json`/`plugin.json` — it's read-only and doesn't touch installed state.
- If a round-trip install test is genuinely necessary, ask first, explain what will change, and clean up afterward (uninstall + marketplace remove) — then verify the cleanup actually restored the prior state, including `~/.claude/settings.json`, not just `known_marketplaces.json`.
- Never reuse the real marketplace/plugin name (`ai-skills-toolkit`) for a throwaway local-path test; it will collide with and can silently overwrite the real registration.
