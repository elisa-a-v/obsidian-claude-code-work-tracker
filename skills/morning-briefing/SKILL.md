---
name: morning-briefing
description: Morning briefing to start the work day. Use when user says "morning briefing", "start my day", "where did I leave off", "what should I work on", or similar requests to get oriented for work.
---

# Morning Briefing

> Key words "MUST", "MUST NOT", "SHOULD", "SHOULD NOT", and "MAY" follow [RFC2119](https://www.rfc-editor.org/rfc/rfc2119).

Help the user start their work day by orienting them on where they left off and what to focus on.

## Instructions

0. **MUST check spoons level**:
   - If user specifies spoons in greeting (e.g., "morning, no spoons"), update the `Current spoons:` value in CLAUDE.md and proceed accordingly
   - If not specified, do a quick check-in: "How are you feeling today?" before proceeding
   - Once confirmed, update the `Current spoons:` value in CLAUDE.md
   - Adjust all subsequent steps based on spoons level (see "Spoons-Based Adjustments" below)

1. **MUST read recent daily notes** (last 3-5 work days):
   - Path pattern: `daily/YYYY/MM/YYYY-MM-DD.md`
   - MUST look at the "To do" section for incomplete tasks (`- [ ]`)
   - MUST look at the "Worklog" section to understand recent work
   - SHOULD note any patterns or ongoing work

2. **MUST check pending PR reviews** from GitHub:
   <!-- CUSTOMIZE: Adjust the criteria for how your team signals "review needed".
        This example uses assignee as the signal — adapt to your team's workflow
        (e.g., review-requested, labels, etc.) -->
   - Find open PRs where you are assigned but NOT the author
   - Check across your repositories
   - These are often top priority — list them in the standup "Today" section

3. **MUST check project board** from GitHub (if applicable):
   <!-- CUSTOMIZE: Replace with your project board URL, or remove if you don't use one -->
   - Identify items assigned to you
   - Note priorities and deadlines if visible

4. **MUST check the task board**:
   - Path: `tasks/Tasks.md`
   - Review Backlog, Next, and In Progress columns
   - Note anything that's ready to pick up or relevant to today's work
   - SHOULD cross-reference with project board items and daily todos to spot overlap or forgotten items

5. **MUST scan recent meeting notes** (last 1-2 weeks):
   - Path: `meetings/` directory
   - Look for action items, decisions, or follow-ups
   - Check if any are still pending

6. **MUST synthesize and present**:
   - MUST start with "Here's where things stand:"
   - MUST summarize what was worked on recently (1-2 sentences)
   - MUST list any incomplete todos from recent days
   - MUST identify natural continuations of yesterday's work
   - SHOULD list pending action items from meetings
   - SHOULD show relevant project board items and task board items
   - MUST end with a clear suggestion: "I'd suggest starting with X because..."

7. **SHOULD help with decision paralysis**:
   - If there are many options, SHOULD help narrow down to 1-2 concrete next steps
   - Consider: urgency, quick wins for momentum, blocked items to unblock
   - MAY ask if the user wants help getting started on the chosen task

8. **MUST generate standup draft** (on standup days only):
   <!-- CUSTOMIZE: Adjust the days to match your team's standup schedule.
        This example uses Monday, Wednesday, Friday. -->
   - MUST check if today is a standup day (Mon, Wed, Fri)
   - If yes, MUST include a ready-to-post standup message at the end
   - Format (standard markdown bold `**text**`):
     ```
     [Greeting - e.g., "Happy Monday!", "Happy Wednesday!", "Happy Friday!"]

     **[Previous day label]:**
     - Item 1
     - Item 2

     **Today:**
     - To do 1
     - To do 2
     ```
   - For "Previous day": MUST use the most recent work day's worklog
     - Monday → use Friday's worklog, label as `*Friday:*`
     - Otherwise → use previous day's worklog, label as `*Yesterday:*`
   - For "Today": MUST use concrete tasks from pending PR reviews, task board, continuations of yesterday's work, and project board items — not generic suggestions
   - MUST write the standup draft to today's daily note under a "## Standup draft" section (before the Worklog section)
   - MUST tell the user where to find it

   **Standup framing guidance:**
   - Keep it simple — only what the team needs to know
   - 2-4 items max per section; combine related work into single lines
   - Short descriptions — brief outcome, not a detailed breakdown
   - Frame in terms of outcomes/impact, not activities
   - Before finalizing, check for gaps or stale info. If uncertain about something specific, ask ONE focused, easy-to-answer question rather than guessing

## Tone

SHOULD be a supportive buddy/mentor. SHOULD keep it concise but warm. The goal is to reduce overwhelm and help the user get moving.

## Spoons-Based Adjustments

The user tracks energy/capacity via `Current spoons:` in CLAUDE.md. Adjust approach accordingly:

**none** (no spoons):
- Maximum support mode
- Skip questions entirely - just present the briefing
- Be very directive: "Here's what to focus on: X"
- Keep everything extremely short
- Offer to skip standup if it's a standup day
- One concrete next step only

**low**:
- Gentle mode
- Draft standup fully, only flag something if it's clearly wrong
- Narrow to 1 suggestion max
- Keep briefing concise
- Be encouraging

**normal** (default):
- Standard mode
- Draft and spot-check
- If uncertain about something specific, ask ONE focused question (concrete, easy to answer)
- Present 1-2 options if relevant

**high**:
- Can engage more collaboratively
- Ask clarifying questions more freely
- Explore options together
- Discuss tradeoffs if helpful
