---
description: Push the current changes and open a detailed, explain-diff-style PR (English)
allowed-tools: Read, Grep, Glob, Bash(git status:*), Bash(git branch:*), Bash(git checkout:*), Bash(git add:*), Bash(git commit:*), Bash(git push:*), Bash(git log:*), Bash(git diff:*), Bash(git show:*), Bash(gh pr create:*), Bash(gh pr view:*), Bash(gh repo view:*), Write
---

Optional title/notes: $ARGUMENTS

Take the current working-tree changes exactly as they are and open a pull
request with a **detailed** body — the same depth and style as the
`explain-diff` command, minus the quiz. Do not refactor, clean up, or "improve"
the diff first.

## Steps

1. Run `git status` and `git diff` to see what will go into the PR. Read the
   surrounding code broadly (Read/Grep/Glob) so the body is grounded in the real
   codebase, not guesses.
2. Determine the current branch. If it is the default branch (`main`/`master`),
   create a new branch first (derive a short kebab-case name from the changes)
   and switch to it. Otherwise stay on the current branch.
3. Stage and commit anything uncommitted with a message that describes the
   actual changes. Do not drop, split, or reword unrelated existing commits.
4. Push the branch to the remote, setting upstream if needed
   (`git push -u origin <branch>`).
5. Write the full PR body to a temp file and create the PR with
   `gh pr create --body-file <tempfile>`. Write the title and body **in English**,
   based on the real diff and commit history. If `$ARGUMENTS` is given, use it as
   the title or as extra context for the body.
6. Print the PR URL and stop.

## PR body structure

The body must contain these sections (no quiz):

### Background

Explain the existing system relevant to this change. Explore surrounding code
broadly. Include two layers:
- A deep background for beginners (note that it can be skipped if already familiar)
- A narrower background directly relevant to the change

### Intuition

Explain the core intuition for the change. Focus on essence, not full details.
Use concrete examples with toy data. Use ASCII diagrams and tables liberally.

### Code

Do a high-level walkthrough of the changes. Group/order the changes in an
understandable way. Show key code snippets.

## Rules

- Do not ask for confirmation or clarifying questions. Push and open the PR
  directly. If anything is ambiguous, assume the obvious default and proceed.
- Ship the current changes as-is — never edit source files to polish the diff.
- If the working tree is clean and the branch is already pushed with no new
  commits vs. the base, say there is nothing to PR instead of creating an empty one.
- Never force-push, never target or push directly to the default branch.
- Write in the clarity and flow of Martin Kleppmann — engaging, classic style,
  smooth transitions between sections.
- Use callouts (blockquotes) for key concepts, definitions, and edge cases.
- Use ASCII diagrams (not images) when helpful.
- End PR bodies with:
  🤖 Generated with [Claude Code](https://claude.com/claude-code)
