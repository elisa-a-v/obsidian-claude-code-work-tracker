---
name: session-log
description: Log the current session's work. Use when user says "log session", "save session", "checkpoint", or proactively when significant work is done that should be captured for end-of-day.
---

# Session Log

> Key words "MUST", "MUST NOT", "SHOULD", "SHOULD NOT", and "MAY" follow [RFC2119](https://www.rfc-editor.org/rfc/rfc2119).

Capture what we've worked on in this session so it persists across sessions and supports the end-of-day wrap-up.

## Instructions

1. **MUST check for existing log today**:
   - Path: `sessions/YYYY/MM/DD.md` (e.g., `sessions/2026/01/08.md`)
   - If it exists, MUST read it to understand what's already documented
   - New entries MUST be inserted in chronological order (earlier first)
   - MUST NOT duplicate existing entries
   - **Existing content is sacred**: MUST NOT remove, replace, or overwrite ANY existing content unless explicitly asked or correcting a known error. When using the Edit tool, `old_string` MUST appear unchanged in `new_string` — only add around it.

2. **MUST gather session context**:
   - What did we work on together in this session?
   - What files were created, edited, or reviewed?
   - What decisions were made?
   - What's still open or unfinished?

3. **MUST insert new entry in session log**:
   - MUST create file if it doesn't exist, with header format:
     ```
     # Session Log - Weekday, [[YYYY-MM-DD]]

     [[sessions/YYYY/MM/prev|< Yesterday]] - [[sessions/YYYY/MM/next|Tomorrow >]]

     ---
     ```
   - MUST insert a new entry in chronological position with timestamp: `## HH:MM`
   - SHOULD include sections as relevant:
     - **Worked on**: Brief summary of tasks/topics
     - **Files touched**: List of files created/edited/reviewed
     - **Decisions**: Any choices made or directions confirmed
     - **Open threads**: Things left unfinished or to revisit
   - SHOULD keep entries concise - bullet points, not prose
   - MUST use links when mentioning PRs or GitHub issues.

4. **SHOULD confirm with user**:
   - Briefly state what was logged
   - If appending, note what's new vs already captured

## File Format Example

```markdown
# Session Log - Monday, [[2025-01-06]]

[[sessions/2025/01/05|< Yesterday]] - [[sessions/2025/01/07|Tomorrow >]]

---

## 09:15

**Worked on**: Updated CLAUDE.md with role info and communication preferences

**Files touched**:
- CLAUDE.md (edited)

**Decisions**:
- Keep vault structure section (saves tokens vs exploring)
- Direct feedback style, no sugarcoating

---

## 14:30

**Worked on**: Created session-log skill

**Files touched**:
- .claude/skills/session-log/SKILL.md (created)
- .claude/skills/end-of-day/SKILL.md (edited)

**Open threads**:
- Test the skill tomorrow morning

---
```
