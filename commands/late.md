---
description: Run a prompt later in this session at a given time
allowed-tools: CronCreate
---

Arguments: $ARGUMENTS

The first token is the fire time in HH:MM format (24-hour, local time).
Everything after it is the prompt to run at that time.

Register a one-shot task with CronCreate using the cron expression
"MM HH * * *" (day-of-month and month stay as `*` wildcards) and
`recurring: false`.

Rules:
- Do not ask for confirmation or clarification.
- Keep day-of-month and month as `*`. Do NOT pin a specific date, and do NOT
  assume tomorrow. Pass `recurring: false` so CronCreate fires once at the NEXT
  occurrence of the time — today if the time has not yet passed, otherwise
  tomorrow. Let the scheduler decide the day; never reason about
  "morning/dawn/night" to pick a day yourself.
- If the given minute is 00 or 30, shift it by one minute to avoid jitter.
- Register the task, report the fire time and task ID in one line, then stop.
