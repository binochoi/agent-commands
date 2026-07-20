---
description: Run a prompt later in this session at a given time
allowed-tools: CronCreate
---

Arguments: $ARGUMENTS

The first token is the fire time in HH:MM format (24-hour, local time).
Everything after it is the prompt to run at that time.

Register a one-shot task with CronCreate using the cron expression
"MM HH * * *" derived from the given time.

Rules:
- Do not ask for confirmation or clarification.
- If the time is ambiguous, assume the next occurrence and proceed.
- If the given minute is 00 or 30, shift it by one minute to avoid jitter.
- Register the task, report the fire time and task ID in one line, then stop.
