<%*
  // Define recurring meeting presets
  // CUSTOMIZE: Replace these with your actual recurring meetings and attendees
  const meetingPresets = {
    "1-1 with Manager": { meetingType: "1-1", participants: ["Manager Name"] },
    "Team Standup": { meetingType: "standup", participants: ["Alice", "Bob", "Charlie"] },
    "Sprint Planning": { meetingType: "sprint-planning", participants: ["Alice", "Bob", "Charlie", "Manager Name"] },
    "Sprint Retro": { meetingType: "sprint-retro", participants: ["Alice", "Bob", "Charlie", "Manager Name"] },
    "Other (manual entry)": null
  };

  const presetNames = Object.keys(meetingPresets);
  const selectedPreset = await tp.system.suggester(presetNames, presetNames);
  if (!selectedPreset) return;

  const preset = meetingPresets[selectedPreset];
  const date = await tp.system.prompt("Date (YYYY-MM-DD)");

  let time, topic, participants, meetingType;

  if (preset) {
    // Recurring meeting
    time = await tp.system.prompt("Time (HH:MM)");
    topic = selectedPreset;
    participants = preset.participants;
    meetingType = preset.meetingType;

    // Prompt for sprint ID on sprint meetings
    if (meetingType === "sprint-planning" || meetingType === "sprint-retro") {
      const sprintId = await tp.system.prompt("Sprint name/ID");
      if (sprintId) topic = `${selectedPreset} - ${sprintId}`;
    }
  } else {
    // Manual entry
    time = await tp.system.prompt("Time (HH:MM)");
    topic = await tp.system.prompt("Subject (required without special chars like ?%&#)");
    meetingType = "other";
    const otherPeopleCount = await tp.system.prompt("How many attendees? (without counting you)");
    const parsedCount = parseInt(otherPeopleCount);
    participants = [];
    for (let i = 0; i < parsedCount; i++) {
      const name = await tp.system.prompt(`Attendee #${i+1} name`);
      if (name) participants.push(name);
    }
  }

  const path = `/meetings/${date} ${topic}`;
  if (date && time && topic) await tp.file.move(path);

  const participantString = participants.map(p => `\n  - ${p}`).join("");
%>---
type: meeting
meeting-type: <% meetingType %>
date: <% date %>
time: <% time %>
summary: <% topic %>
participants:<% participantString %>
---

[[<% date %>|Go to day >]]

