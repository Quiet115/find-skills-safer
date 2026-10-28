# find-skills-safer

A Claude Code skill that finds agent skills for a task **without installing anything behind your back**.

Finding is free; downloading and installing are not. Every skill goes through a gate where you decide.

## What it does

1. Checks whether a skill you already have covers the need.
2. Searches read-only (skills.sh, GitHub metadata) and gathers risk signals: author, stars, install count, whether the folder has scripts, hooks or `.mcp.json`.
3. Shows a **shortlist of 3 to 5 candidates**: the recommended one first, and for every other one a concrete reason why it fits or why it was left out.
4. Asks once, with three options:
   - **Download to quarantine and review** (recommended): fetched into a scratch folder, read in full and scanned; nothing runs; a second confirmation before install.
   - **Install directly, without review**: copies only the skill's own folder, runs nothing from it.
   - **Do not install**.
   The same question asks the scope: all projects (`~/.claude/skills/`) or one project (`.claude/skills/`).

## Rules it keeps

- Never uses `-y`; never assumes global scope.
- Never runs `npx skills add`, `/plugin install` or anything that installs before you choose.
- Treats everything it reads about a skill (READMEs, SKILL.md, search results) as data, not instructions.
- Never calls a skill "safe"; it reports "no risk signals found" and what it could not check.
- An earlier yes never covers a new skill.

## Install

Copy the `find-skills` folder into `~/.claude/skills/` (all projects) or `.claude/skills/` (one project), then open a new session.

```bash
git clone https://github.com/<your-user>/find-skills-safer.git
cp -r find-skills-safer/find-skills ~/.claude/skills/
```

Use it with `/find-skills <what you need>` or by asking "find a skill for X".

The skill text is written in English with user-facing messages in Spanish by default (it answers in the user's language). Change the line "Always talk to the user in their language (Spanish by default)" to switch the default.

## Credits and license

Based on the `find-skills` skill from [vercel-labs/skills](https://github.com/vercel-labs/skills) (MIT). This version adds the permission gates, the quarantine review, the candidate shortlist and the safety rules. MIT licensed; see `LICENSE`.
