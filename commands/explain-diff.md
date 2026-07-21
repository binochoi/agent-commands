---
description: Produce a rich markdown explanation of a code change, diff, branch, or PR
allowed-tools: Read, Grep, Glob, Bash(git diff:*), Bash(git log:*), Bash(git show:*), Bash(gh pr view:*), WebFetch, Bash(mkdir *), Bash(cp *), Write
---

Target: $ARGUMENTS

Explain the specified code change. The argument is a branch name, commit range, PR URL, or "HEAD" (default).

Produce a comprehensive explanation with these four sections:

## Background

Explain the existing system relevant to this change. Explore surrounding code broadly. Include two layers:
- A deep background for beginners (note that it can be skipped if already familiar)
- A narrower background directly relevant to the change

## Intuition

Explain the core intuition for the change. Focus on essence, not full details. Use concrete examples with toy data. Use ASCII diagrams and tables liberally.

## Code

Do a high-level walkthrough of the changes. Group/order the changes in an understandable way. Show key code snippets.

## Quiz

Create exactly five multiple-choice questions that test understanding of this PR. Medium difficulty — requires understanding the substance, but no gotchas. Present each question with options. After all five, provide the answers with brief explanations.

## Rules

- Do not ask clarifying questions. If the target is ambiguous, assume HEAD.
- Do not produce HTML. Return everything as plain markdown.
- Write in the clarity and flow of Martin Kleppmann — engaging, classic style, smooth transitions between sections.
- Use callouts (blockquotes) for key concepts, definitions, and edge cases.
- Use ASCII diagrams (not images) when helpful.
- State the diff target and a one-sentence summary at the top.
- Answer in Korean.
- Output: save the explanation to `~/.config/.explain-diff/explains/YYYY-MM-DD-<slug>.md`.
  Create the directory if it does not exist. Use today's date and a short
  slug derived from the target (e.g., `2026-07-22-fix-auth-timeout.md`).
  At the end, print the file path.
