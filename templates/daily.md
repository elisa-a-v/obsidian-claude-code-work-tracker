<%*
// This template requires the following community plugins:
// - Templater
//   - Enable the option 'Trigger Templater on new file creation'.
// - Dataview
//   - JavaScript queries must be enabled.
// - Periodic Notes.
//   - Enable Daily Notes and enter this template's path.
//   - The filename must be in the format YYYY-MM-DD, but it is
//     recommended to use YYYY/MM/YYYY-MM-DD to keep things organized.

// For meetings to be picked up, the notes need to:
// - Be under the `/meetings/` dir.
// - Have `type: meeting` in frontmatter.
// - Have the fields `time` and `participants` in frontmatter.

// For tasks to be picked up by the Upcoming Deadlines section:
// - Be under the `/tasks/` dir.
// - Have a `due` field in frontmatter (YYYY-MM-DD format).
// - Tasks on the kanban board (tasks/Tasks.md) use column position as
//   source of truth — items in the "Done" column are excluded.
// - Tasks not on the board fall back to a `completed` frontmatter field.

const getFormatted = (to, from) => tp.date.now(to, 0, tp.file.title, from);
const date = getFormatted("dddd, LL", "YYYY-MM-DD");
const date_string = date.charAt(0).toUpperCase() + date.slice(1);
%># <% date_string %>

📝 [[sessions/<% getFormatted("YYYY/MM/DD", "YYYY-MM-DD") %>|Session log]]

[[<% tp.date.now("YYYY-MM-DD", -1, tp.file.title, "YYYY-MM-DD") %>|< Yesterday]] - [[<% tp.date.now("YYYY-MM-DD", 1, tp.file.title, "YYYY-MM-DD") %>|Tomorrow >]]

----

## Meetings
```dataviewjs
const thisNote = dv.current();

const thisNotesDay = thisNote.file.day?.toISODate();
const meetings = dv.pages(
    '"meetings"'
).where(
  m => (m.type === "meeting"
              && m.date?.toISODate() == thisNotesDay)
);

// Check whether we got any results:
if (meetings.length > 0) {
// If yes, render a table
    dv.table(["Subject", "Time", "Participants"], meetings.map(m => [m.file.link, m.time, m.participants]));
} else {
    // If not, show a fallback message
    dv.paragraph("No meetings today!");
}
```

---

## Upcoming deadlines
```dataviewjs
const today = dv.current().file.day;

// Parse kanban board to check completion status by column
const kanban = await dv.io.load("tasks/Tasks.md");
const doneSection = kanban.match(/## Done\n([\s\S]*?)(?=\n## |\n%%|$)/)?.[1] ?? "";
const isOnBoard = (name) => kanban.includes(`[[${name}`);
const isDone = (name) => doneSection.includes(`[[${name}`);

const tasks = dv.pages('"tasks"')
  .where(t => {
    if (!t.due || dv.date(t.due) === null) return false;
    const name = t.file.name;
    // If on the board, use column as source of truth
    if (isOnBoard(name)) return !isDone(name);
    // If not on the board, fall back to frontmatter
    return !t.completed;
  })
  .sort(t => t.due, 'asc');

const overdue = tasks.where(t => dv.date(t.due) < today);
const upcoming = tasks.where(t => {
  const due = dv.date(t.due);
  return due >= today && due <= today.plus({days: 7});
});

const fmt = (t) => {
  const name = t.file.aliases?.[0] ?? t.file.name;
  const link = dv.fileLink(t.file.path, false, name);
  const due = dv.date(t.due).toFormat("MMM d");
  return `${link} — due ${due}`;
};

if (overdue.length > 0) {
  dv.header(4, "⚠️ Overdue");
  dv.list(overdue.map(fmt));
}
if (upcoming.length > 0) {
  dv.header(4, "📅 Next 7 days");
  dv.list(upcoming.map(fmt));
}
if (overdue.length === 0 && upcoming.length === 0) {
  dv.paragraph("No upcoming deadlines.");
}
```

---

## To do

- [ ] Standup

---

## Worklog

-
