# Setup Guide

This guide walks you through setting up the work tracking system from scratch.

## Prerequisites

- [Obsidian](https://obsidian.md/) installed
- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) installed
- Git (for version control of your vault)

## 1. Create your vault

This repo is set up as a [GitHub template](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template). Create a new repo from it (or clone it directly), then open it as an Obsidian vault:

1. Click **"Use this template"** on the repo page to create your own copy, then clone it: `git clone <your-repo-url> ~/my-work-vault`
2. Open Obsidian → "Open folder as vault" → select the directory
3. When prompted about community plugins, enable them (you'll install them next)

## 2. Install Obsidian plugins

Install these community plugins (Settings → Community plugins → Browse):

### Required

- **[Templater](https://github.com/SilentVoid13/Templater)** — Automates file creation with the right structure and metadata
- **[Dataview](https://github.com/blacksmithgu/obsidian-dataview)** — Powers the dynamic meetings table and deadline tracker in daily notes
- **[Kanban](https://github.com/mgmeyers/obsidian-kanban)** — Visual task board (the `Tasks.md` file)
- **[Periodic Notes](https://github.com/liamcain/obsidian-periodic-notes)** — Creates daily notes on a schedule

### Optional

- **[Calendar](https://github.com/liamcain/obsidian-calendar-plugin)** — Sidebar calendar widget for navigating daily notes

## 3. Configure plugins

### Templater

1. Settings → Templater → **Template folder location**: `templates`
2. Enable **Trigger Templater on new file creation**
3. Under **Startup Templates**, add: `templates/startup.md`
   - This auto-opens today's daily note when you launch Obsidian (skips weekends)

### Periodic Notes

1. Settings → Periodic Notes → Enable **Daily Notes**
2. Set **Daily Note Template**: `templates/daily.md`
3. Set **Date Format**: `YYYY-MM-DD`
4. Set **New File Location**: `daily/YYYY/MM` (creates organized year/month folders)

### Dataview

1. Settings → Dataview → Enable **JavaScript Queries**
   - Required for the meetings table and deadline tracker in daily notes

### Kanban

No special configuration needed — just open `tasks/Tasks.md` and it renders as a board automatically.

## 4. Create vault directories

Create these directories in your vault if they don't already exist:

```
mkdir -p daily sessions tasks meetings
```

## 5. Install Claude Code skills

The skills define the three daily routines (morning briefing, session logging, end-of-day). Copy them to your Claude Code skills directory:

```bash
# Create the skills directory if it doesn't exist
mkdir -p ~/.claude/skills

# Copy skills from this repo
cp -r skills/morning-briefing ~/.claude/skills/
cp -r skills/session-log ~/.claude/skills/
cp -r skills/end-of-day ~/.claude/skills/
```

## 6. Customize CLAUDE.md

Open `CLAUDE.md` in the vault root and replace all `[CUSTOMIZE]` placeholders with your own details:

- Your role, team, manager
- Your GitHub username
- Your project board URL (if any)
- Your repositories (if doing development work through this vault)

The rest of the file (spoons system, communication style, session logging rules) can be used as-is or adjusted to your preferences.

## 7. Customize the morning briefing

Open `~/.claude/skills/morning-briefing/SKILL.md` and look for `<!-- CUSTOMIZE -->` comments:

- **PR review criteria**: How does your team signal "your review is needed"? Adjust the check accordingly.
- **Project board**: Add your board URL or remove the step if you don't use one.
- **Standup days**: Change from Mon/Wed/Fri to whatever your team uses.

## 8. Customize the meeting template

Open `templates/meeting.md` and replace the example recurring meetings with your actual ones. The presets save time — instead of typing attendees every time, you pick from a list.

## Verification

Once everything is set up:

1. **Test daily note creation**: Use the Command Palette → "Periodic Notes: Open daily note" — it should create today's note with the full template (meetings table, deadlines, to-do, worklog sections)
2. **Test the kanban board**: Open `tasks/Tasks.md` — it should render as a drag-and-drop board
3. **Test Claude Code**: Open a terminal in your vault directory and run `claude`. Try saying "morning briefing" — it should read your daily notes, check GitHub, and give you a summary.

## Daily usage

Once set up, the daily routine is:

1. **Open Obsidian** — the startup template auto-opens today's daily note
2. **Run morning briefing** — `claude` → "morning briefing"
3. **Work** — Claude logs session checkpoints as you go
4. **End of day** — "end of day" → Claude updates your daily note, moves tasks, offers to commit

See the `examples/` directory for what filled-in daily notes and session logs look like.
