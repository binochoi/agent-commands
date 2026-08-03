---
description: Push the current changes and open a PR as-is
allowed-tools: Bash(git status:*), Bash(git branch:*), Bash(git checkout:*), Bash(git add:*), Bash(git commit:*), Bash(git push:*), Bash(git log:*), Bash(git diff:*), Bash(gh pr create:*), Bash(gh pr view:*), Bash(gh repo view:*), Bash(ps:*), Bash(kill:*)
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
5. Create the PR with `gh pr create`. Write the title and body **in Korean**,
   based on the real diff and commit history. If `$ARGUMENTS` is given, use it
   as the title or as extra context for the body.
6. Print the PR URL.
7. **As the very last action** (only if the PR was actually created
   successfully in step 5), terminate the terminal session by walking up the
   process tree to the `login` (session-leader) ancestor and killing it:

   ```bash
   pid=$$
   while [ -n "$pid" ] && [ "$pid" != "1" ]; do
     ppid=$(ps -o ppid= -p "$pid" 2>/dev/null | tr -d ' ')
     [ -z "$ppid" ] && break
     case "$(ps -o comm= -p "$ppid" 2>/dev/null)" in
       *login) kill -TERM "$ppid"; break ;;
     esac
     pid="$ppid"
   done
   ```

   This ends the Claude session and closes the terminal tab/window. Do not
   print anything after this step.

## Rules

- Do not ask for confirmation or clarifying questions. Push and open the PR
  directly. If anything is ambiguous, assume the obvious default and proceed.
- Ship the current changes as-is — never edit source files to polish the diff.
- If the working tree is clean and the branch is already pushed with no new
  commits vs. the base, say there is nothing to PR instead of creating an empty one.
- Never force-push, never target or push directly to the default branch.
- The terminate step (step 7) is a hard `kill`, not a graceful exit — the
  session ends immediately when it runs. Only run it after the PR is confirmed
  created. If the working tree is clean / there is nothing to PR, or any step
  fails, do NOT run it: just stop normally.
- End PR bodies with:
  🤖 Generated with [Claude Code](https://claude.com/claude-code)
