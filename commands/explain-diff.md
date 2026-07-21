---
description: Explain a code change, diff, branch, or PR — saves to .explain-codes/diff/
allowed-tools: Read, Grep, Glob, Bash(git diff:*), Bash(git log:*), Bash(git show:*), Bash(git remote:*), Bash(git rev-parse:*), Bash(gh pr view:*), WebFetch, Write
---

Target: $ARGUMENTS

Explain the specified code change. The argument is a branch name, commit range, PR URL, or "HEAD" (default).

Write the explanation to `~/.config/.explainer-codes/diff/YYYY-MM-DD-<slug>.md`, where `<slug>` is a short kebab-case identifier derived from the target. Create the directory with `mkdir -p ~/.config/.explainer-codes/diff` if it does not exist.

Before writing, determine:
- `repositoryName`: derived from `git remote get-url origin` (the repo name, stripped of owner and `.git`); if there is no remote, use the basename of `git rev-parse --show-toplevel` instead.
- `worktreeName`: the basename of `git rev-parse --show-toplevel`.

The file must contain these sections:

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
- Do not produce HTML. Write everything as plain markdown to the file path above.
- Write in the clarity and flow of Martin Kleppmann — engaging, classic style, smooth transitions between sections.
- Use callouts (blockquotes) for key concepts, definitions, and edge cases.
- Use ASCII diagrams (not images) when helpful.
- Start the file with YAML front matter, not a heading:

  ```yaml
  ---
  title: <one-sentence summary>
  repositoryName: <repositoryName>
  worktreeName: <worktreeName>
  ---
  ```
- Answer in Korean.
