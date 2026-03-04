# Example: Daily Note

> This is an example of what a filled-in daily note looks like. In practice,
> this file is generated automatically by the `daily.md` template — you won't
> write it by hand. The Meetings and Upcoming Deadlines sections are rendered
> by Dataview queries (shown here as static text for illustration).

---

# Wednesday, March 5, 2025

📝 [[sessions/2025/03/05|Session log]]

[[2025-03-04|< Yesterday]] - [[2025-03-06|Tomorrow >]]

----

## Meetings

| Subject | Time | Participants |
|---------|------|-------------|
| [[2025-03-05 1-1 with Manager\|1-1 with Manager]] | 10:00 | Manager Name |
| [[2025-03-05 Sprint Planning\|Sprint Planning]] | 14:00 | Alice, Bob, Charlie, Manager Name |

---

## Upcoming deadlines

#### 📅 Next 7 days
- [[migrate-auth-service|Migrate auth service]] — due Mar 10

---

## Standup draft

Happy Wednesday!

**Yesterday:**
- Reviewed [#142](https://github.com/your-org/your-repo/pull/142) (search refactor)
- Fixed staging deployment issue ([#89](https://github.com/your-org/your-repo/issues/89))

**Today:**
- Continue [#95](https://github.com/your-org/your-repo/issues/95) — search performance fix
- Sprint planning

---

## To do

- [x] Standup
- [x] Review [#142](https://github.com/your-org/your-repo/pull/142)
- [ ] Write tests for search fix
- [ ] Follow up with Alice on API schema question

---

## Worklog

- Reviewed [#142](https://github.com/your-org/your-repo/pull/142) — search refactor, approved with minor comments on error handling
- Fixed staging deploy ([#89](https://github.com/your-org/your-repo/issues/89)) — was a missing env var in the new config
- Sprint planning: picked up [#95](https://github.com/your-org/your-repo/issues/95) (search perf) and [#103](https://github.com/your-org/your-repo/issues/103) (auth migration) for the sprint
- Started digging into search performance — query plan shows missing index on `last_updated`, wrote migration but haven't tested yet
