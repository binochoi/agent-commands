---
description: Register the plan to work on as a GitHub issue in this repo
allowed-tools: Bash(git status:*), Bash(git branch:*), Bash(git log:*), Bash(git diff:*), Bash(gh issue create:*), Bash(gh issue edit:*), Bash(gh issue view:*), Bash(gh repo view:*), Bash(gh label list:*)
---

Plan/topic to register: $ARGUMENTS

Take the plan for the work to be done and register it as a GitHub issue on the
current repo. This is about *upcoming work*, not existing changes — describe what
should be done, not a diff.

If `$ARGUMENTS` points at an existing issue (a `#N` reference, a bare issue
number, or an issue URL), **update that issue** instead of creating a new one —
see "Updating an existing issue" below.

## Steps

1. Figure out what plan to register:
   - If `$ARGUMENTS` names an existing issue (`#N`, a bare number, or an issue
     URL), switch to update mode (see "Updating an existing issue"). Any text
     after the reference is extra guidance for the update.
   - Otherwise, if `$ARGUMENTS` is given, use it as the topic/title of the plan.
   - Otherwise, use the plan already established in this conversation (the plan
     mode plan, a design just discussed, or the agreed next steps).
   - If there is no clear plan and no `$ARGUMENTS`, say there is nothing to
     register instead of inventing one.
2. Confirm the target repo with `gh repo view` so the issue lands on the right
   GitHub repository.
3. Flesh the plan into a proper issue body: a short summary, the concrete tasks
   (as a checklist when there are multiple steps), and any relevant context,
   files, or acceptance criteria. Ground it in the actual codebase, not
   guesses.
4. Create the issue with `gh issue create`. Write the title and body **in
   Korean**. Add labels only if fitting ones already exist (check
   `gh label list`); do not create new labels.
5. Print the issue URL and stop.

## Updating an existing issue

When `$ARGUMENTS` targets an existing issue:

1. Read the current issue with `gh issue view <N>` (include the body) to use it
   as the base.
2. Produce an updated title/body: keep what still applies, and fold in the
   current conversation plan (plus any extra guidance in `$ARGUMENTS`). Ground it
   in the actual codebase, not guesses. Do not blindly discard existing content.
3. Apply the update with `gh issue edit <N> --body <body>` (add `--title` only
   if the title should change). Keep the title and body **in Korean**.
4. Print the issue URL and stop.

## Rules

- Do not ask for confirmation or clarifying questions. Register or update the
  issue directly. If anything is ambiguous, assume the obvious default and
  proceed.
- Do not write, edit, or commit any code — this only creates or updates the
  issue.
- Describe the work as a plan (what to do), not as a completed change.
- 본문은 쉬운 한글로 쓴다. 영어 약어·외래어(TL;DR 등) 대신 쉬운 우리말로 풀어
  쓰고, 어려운 말보다 누구나 아는 쉬운 말을 고른다.
- End issue bodies with:
  🤖 Generated with [Claude Code](https://claude.com/claude-code)
