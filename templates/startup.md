<%*
// Startup template: triggers Periodic Notes to create/open today's daily note.
// This respects all Periodic Notes settings (template, folder, format, etc.)
// Skips weekends (0 = Sunday, 6 = Saturday).
//
// Setup: In Templater settings, go to "Startup Templates" and add this file's
// path. It will run automatically every time Obsidian opens.
// Note: This is separate from "Trigger Templater on new file creation" —
// startup templates run on app launch, not on file creation.

const dayOfWeek = new Date().getDay();
const isWeekend = dayOfWeek === 0 || dayOfWeek === 6;

if (!isWeekend) {
    await app.commands.executeCommandById("periodic-notes:open-daily-note");
}
%>
