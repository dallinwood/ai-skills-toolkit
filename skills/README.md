Each skill lives in its own directory here, named after the skill, containing a `SKILL.md`:

```
skills/
  <skill-name>/
    SKILL.md
    (any supporting scripts, references, or assets)
```

`SKILL.md` needs YAML frontmatter with `name` and `description` — see the other skills in this repo, or the `skill-creator` plugin, for the format. Skills are discovered automatically; nothing else needs to be registered.
