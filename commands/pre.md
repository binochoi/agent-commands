---
description: Push the current changes and open a PR as-is (English)
allowed-tools: Bash(git status:*), Bash(git branch:*), Bash(git checkout:*), Bash(git add:*), Bash(git commit:*), Bash(git push:*), Bash(git log:*), Bash(git diff:*), Bash(gh pr create:*), Bash(gh pr view:*), Bash(gh repo view:*)
---

Optional title/notes: $ARGUMENTS

Take the current working-tree changes exactly as they are and open a pull
request. Do not refactor, clean up, or "improve" the diff first.

## Steps

1. Run `git status` and `git diff` to see what will go into the PR.
2. Determine the current branch. If it is the default branch (`main`/`master`),
   create a new branch first (derive a short kebab-case name from the changes)
   and switch to it. Otherwise stay on the current branch.
3. Stage and commit anything uncommitted with a message that describes the
   actual changes. Do not drop, split, or reword unrelated existing commits.
4. Push the branch to the remote, setting upstream if needed
   (`git push -u origin <branch>`).
5. Create the PR with `gh pr create`. Write the title and body **in English**,
   based on the real diff and commit history. If `$ARGUMENTS` is given, use it
   as the title or as extra context for the body.
6. Print the PR URL and stop.

## Rules

- Do not ask for confirmation or clarifying questions. Push and open the PR
  directly. If anything is ambiguous, assume the obvious default and proceed.
- Ship the current changes as-is — never edit source files to polish the diff.
- If the working tree is clean and the branch is already pushed with no new
  commits vs. the base, say there is nothing to PR instead of creating an empty one.
- Never force-push, never target or push directly to the default branch.
- End PR bodies with:
  🤖 Generated with [Claude Code](https://claude.com/claude-code)
