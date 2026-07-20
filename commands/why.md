---
description: Explain why a specific line of code exists
allowed-tools: Read, Grep, Glob, Bash(git log:*), Bash(git blame:*), Bash(git show:*)
---

Target: $ARGUMENTS

The argument is a path, optionally followed by :LINE or :START-END.

Trace the history of that code:
- Run git log -L on the line range to get its full change history.
- Run git blame to identify the introducing commit.
- Read the introducing commit message and its full diff with git show.
- Search the codebase for related references, tests, and issue numbers.

Rules:
- Do not ask clarifying questions. If no line is given, treat the whole file.
- Answer the question "why does this exist" first, in one paragraph.
- Then list the commits that shaped it, oldest first, with dates and subjects.
- If the history does not explain the intent, say so plainly
  instead of inventing a rationale.
