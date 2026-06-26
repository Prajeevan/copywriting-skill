# AGENTS.md — how to update & ship this skill

Guidance for any AI agent (or human) editing this repo. This is the **copywriting** Agent Skill, published via [skills.sh] and installed with `npx skills add Prajeevan/copywriting-skill`.

## The two locations that matter

| Path | Role |
| --- | --- |
| `skills/copywriting/SKILL.md` (this repo) | **Source of truth.** Tracked in git, pushed to GitHub, distributed by skills.sh. |
| `~/.agents/skills/copywriting/SKILL.md` | **The live copy** Claude Code loads on this machine. `~/.claude/skills/copywriting` is a symlink to `~/.agents/skills/copywriting`, so editing/replacing the file here is enough — no symlink step. |

These two can drift. Always treat the repo file as canonical and push changes from it.

## Going-live methodology (run every time you change the skill)

1. **Edit the source of truth:** `skills/copywriting/SKILL.md` in this repo. Keep the YAML frontmatter (`name`, `description`) intact — the `description` is what makes the skill trigger, so don't bloat or break it.
2. **Sync to the live local path** so this machine's agent uses it immediately:
   ```bash
   cp skills/copywriting/SKILL.md ~/.agents/skills/copywriting/SKILL.md
   diff -q skills/copywriting/SKILL.md ~/.agents/skills/copywriting/SKILL.md   # expect identical
   ```
3. **Keep `README.md` in sync** — its "What's inside" and "Credit" sections must reflect the actual sections and sources in `SKILL.md`.
4. **Commit + push** (branch is `master`, remote `origin` → `github.com/Prajeevan/copywriting-skill`):
   ```bash
   git add -A && git commit -m "<what changed>" && git push
   ```
5. **Downstream consumers update** by re-running `npx skills add Prajeevan/copywriting-skill` to pull the latest published version.

## Don't

- **Don't commit the skill into the home-directory repo.** `~` (`/Users/<user>`) is itself a git repo with **no remote**, and `~/.agents` is untracked there. The *only* tracked, publishable source is **this** repo. Committing into the home repo publishes nothing and creates a confusing second copy.
- **Don't edit only `~/.agents/...`** and consider it "done" — that updates this machine but never reaches GitHub or skills.sh.

## Quick verify

```bash
# Are repo and live copy identical?
diff -q skills/copywriting/SKILL.md ~/.agents/skills/copywriting/SKILL.md
# Is the working tree clean / pushed?
git status --short && git log --oneline -1
```

[skills.sh]: https://skills.sh
