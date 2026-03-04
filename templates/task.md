<%*
  const title = await tp.system.prompt("Task title");
  const origin = await tp.system.prompt("Origin (where this came from)");
  const due = await tp.system.prompt("Due date (YYYY-MM-DD, leave blank if none)");
  const path = `/tasks/${title}`;
  await tp.file.move(path);
%>---
<% due ? `due: ${due}` : `due:` %>
---
# <% title %>

**Origin**: <% origin %>

## Problem

## Notes

## Next steps

- [ ]
