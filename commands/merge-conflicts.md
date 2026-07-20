---
description: Resolve current git merge conflicts; ask when ambiguous
allowed-tools: Bash(git status:*), Bash(git diff:*), Bash(git add:*), Bash(git log:*), Read, Edit, Grep
---

Resolve the merge conflicts in the current repository.

## Steps

1. Run `git status` and list every conflicted file.
2. For each conflict hunk, read enough surrounding context (and `git log` on both sides if needed) to understand the intent of each change.
3. Classify each hunk:
   - **Clear** — resolve it yourself. Examples: both sides add independent imports, functions, or list entries; one side is a pure formatting or rename change; one side is a strict superset of the other; a lockfile or generated file that can be regenerated.
   - **Ambiguous** — do NOT guess. Examples: both sides edit the same logic differently; conflicting business rules, constants, or config values; changes whose correctness depends on intent you cannot infer; schema or migration conflicts.
4. Apply the clear resolutions. Remove all conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`) and keep the result syntactically valid.
5. Stop and ask about the ambiguous ones. For each, report in this format:

```
   File: path/to/file.ts (lines X-Y)
   Ours:   <short summary + code>
   Theirs: <short summary + code>
   Why ambiguous: <one line>
   Options: (a) keep ours (b) keep theirs (c) merge both — <proposed merge>
```

6. After my answers, apply them, then `git add` only the files you resolved.

## Rules

- Never run `git commit`, `git merge --abort`, or `git checkout --ours/--theirs` on a whole file without asking.
- Never invent code that exists on neither side unless it is required to merge both behaviors, and say so explicitly.
- If a file has both clear and ambiguous hunks, resolve the clear ones and still ask about the rest.
- End with a summary: files auto-resolved, files pending my decision, files still unstaged.
