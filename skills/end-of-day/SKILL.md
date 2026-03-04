---
name: end-of-day
description: End of day wrap-up to close out the work day. Use when user says "end of day", "wrap up", "close my day", "log my work", or similar requests to finish working.
---

# End of Day Wrap-up

> Key words "MUST", "MUST NOT", "SHOULD", "SHOULD NOT", and "MAY" follow [RFC2119](https://www.rfc-editor.org/rfc/rfc2119).

Help the user close out their work day by capturing what was done and setting up for tomorrow.

## Instructions

1. **MUST gather the day's work from multiple sources**:
   - **Session log**: MUST read `sessions/YYYY/MM/DD.md` for today - this captures work done across all Claude sessions
   - **Current session**: MUST reference what we did together in this session (may not be logged yet)
   - **Today's daily note**: MUST check `daily/YYYY/MM/YYYY-MM-DD.md` for existing entries
   - SHOULD ask the user what else they worked on if anything seems missing

2. **MUST update the To do checklist**:
   - MUST cross-reference the "To do" section against the session log and current session
   - MUST check off (`- [x]`) any items that were completed, including nested items
   - If a to-do item was partially done, SHOULD leave it unchecked and note progress in the worklog
   - MUST update the daily note file directly (don't just propose changes)

3. **MUST help write the Worklog**:
   - Today's daily note is at: `daily/YYYY/MM/YYYY-MM-DD.md`
   - The Worklog section uses bullet points
   - MUST use `[#123](url)` format for all PR and issue references — never bare `#123`
   - The worklog captures highlights; the session log has full detail. Use judgement about what's worth calling out.
   - SHOULD include: PRs opened/reviewed/merged, issues worked on, meetings attended, blockers encountered
   - SHOULD offer to update the file directly or provide text to copy

4. **MUST capture loose ends**:
   - MUST review "Open threads" from session log
   - MUST ask: "Anything you want to remember for tomorrow?"
   - MUST identify tasks that were started but not finished
   - MUST note any blockers or things waiting on others

5. **MUST review the task board**:
   - Path: `tasks/Tasks.md`
   - MUST cross-reference today's work against Backlog, Next, and In Progress columns
   - MUST move completed items to Done
   - SHOULD move items that were started today into In Progress
   - SHOULD ask about any In Progress items that weren't touched — still active, or should they move back?
   - MAY suggest adding new items discovered during the day (from meeting action items, loose ends, etc.)
   - MUST update the file directly after confirming changes with user

6. **SHOULD set up tomorrow**:
   - MAY offer to add items to tomorrow's "To do" section
   - If there's a clear "start here" point, SHOULD note it prominently
   - MAY suggest creating/updating issue notes for complex ongoing work

7. **SHOULD check meeting follow-ups**:
   - If meetings happened today, SHOULD ask if there are action items to capture
   - MAY offer to update meeting notes with any missing information

8. **MUST offer to commit vault changes**:
   - MUST check `git status` in the vault directory
   - If there are uncommitted changes, MUST ask: "Ready to commit today's vault changes?"
   - If confirmed:
     <!-- CUSTOMIZE: The commands below assume standard git. If you use aliases,
          adjust accordingly (e.g., `git add -p` for interactive staging,
          `git commit -m "..."` for committing). -->
     - MUST prompt user to stage changes (e.g., `git add -p` for interactive staging, or `git add <files>`)
     - MUST wait for them to finish staging
     - SHOULD suggest a brief summary based on today's work (don't ask, just propose one)
     - MUST use `git commit -m "EOD: YYYY-MM-DD - <summary>"` to commit
   - If no changes, SHOULD skip this step silently

## Tone

SHOULD keep it quick and low-friction. The user is wrapping up, so SHOULD be efficient. MAY celebrate small wins without being over the top. The goal is to leave them feeling organized, not overwhelmed.
