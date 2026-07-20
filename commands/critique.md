---
description: Review recent work as a hostile third-party reviewer
allowed-tools: Read, Grep, Glob, Bash(git diff:*), Bash(git log:*)
---

Current diff:
!`git diff HEAD`

Review the changes above as an external reviewer who did not write them.

Rules:
- List problems only. No praise, no summary of what the code does.
- Order findings by severity: correctness, then security, then maintainability.
- For each finding give the file, the line, the concrete failure mode,
  and the smallest fix that resolves it.
- If a finding is a guess, label it as unverified rather than asserting it.
- If there are no real problems, say so in one line and stop.
