# CLAUDE.md

This repo is the **copywriting** Agent Skill (published via [skills.sh], installed with `npx skills add Prajeevan/copywriting-skill`).

**Before editing or shipping the skill, read [`AGENTS.md`](AGENTS.md)** — it holds the full going-live methodology. The essentials:

- **Source of truth:** `skills/copywriting/SKILL.md` in this repo (tracked, pushed to `github.com/Prajeevan/copywriting-skill`, branch `master`).
- **Live copy on this machine:** `~/.agents/skills/copywriting/SKILL.md` (Claude Code loads this; `~/.claude/skills/copywriting` is a symlink to it).

## Going live (every change)

1. Edit `skills/copywriting/SKILL.md` here. Keep the frontmatter `description` intact — it controls skill triggering.
2. Sync to the live path: `cp skills/copywriting/SKILL.md ~/.agents/skills/copywriting/SKILL.md`
3. Keep `README.md` ("What's inside" + "Credit") in sync with the actual sections/sources.
4. `git add -A && git commit -m "<what changed>" && git push`
5. Consumers re-run `npx skills add Prajeevan/copywriting-skill` to pull the update.

## Don't

- Don't commit the skill into the home-directory git repo (`~` is a repo with no remote; `~/.agents` is untracked there). **This** repo is the only publishable source.
- Don't edit only `~/.agents/...` — that updates this machine but never reaches GitHub / skills.sh.

[skills.sh]: https://skills.sh
