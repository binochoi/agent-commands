---
description: Register the plan as a detailed, explain-plan-style GitHub issue
allowed-tools: Read, Grep, Glob, Bash(git status:*), Bash(git branch:*), Bash(git log:*), Bash(git diff:*), Bash(git remote:*), Bash(git rev-parse:*), Bash(gh issue create:*), Bash(gh issue edit:*), Bash(gh issue view:*), Bash(gh repo view:*), Bash(gh label list:*), Write
---

Plan/topic to register: $ARGUMENTS

Take the plan for the work to be done and register it as a GitHub issue on the
current repo, with a **detailed** body — the same depth and style as the
`explain-plan` command, minus the quiz. This is about *upcoming work*, not
existing changes — describe what should be done, not a diff.

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
2. Ground the plan in the codebase — read the surrounding code broadly
   (Read/Grep/Glob, `git log`/`git diff`) so the issue reflects reality, not
   guesses.
3. Confirm the target repo with `gh repo view` so the issue lands on the right
   GitHub repository.
4. Write the full issue body to a temp file and create the issue with
   `gh issue create --body-file <tempfile>`. Write the title and body **in
   Korean**. Add labels only if fitting ones already exist (check
   `gh label list`); do not create new labels.
5. Print the issue URL and stop.

## Updating an existing issue

When `$ARGUMENTS` targets an existing issue:

1. Read the current issue with `gh issue view <N>` (include the body) to use it
   as the base.
2. Ground the update in the codebase (Read/Grep/Glob, `git log`/`git diff`), the
   same as a fresh issue.
3. Produce an updated detailed body using the same section structure below: keep
   what still applies, and fold in the current conversation plan (plus any extra
   guidance in `$ARGUMENTS`). Do not blindly discard existing content.
4. Write the updated body to a temp file and apply it with
   `gh issue edit <N> --body-file <tempfile>` (add `--title` only if the title
   should change). Keep the title and body **in Korean**.
5. Print the issue URL and stop.

## Issue body structure

The body must contain these sections (no quiz):

### 배경 (Context)

Describe the problem this plan addresses. What is broken, missing, or
suboptimal? What prior solutions or discussions exist in the codebase (issues,
prior PRs, TODO comments)? Include both high-level business context and
technical context.

### 설계 (Design)

Explain the proposed solution. Cover:
- Core idea and key design decisions
- Trade-offs (what was considered and rejected, and why)
- Data model, API surface, or component architecture — whichever is relevant
Use ASCII diagrams and tables liberally.

### 구현 계획 (Implementation Plan)

Break the work into ordered steps (use a checklist when there are multiple
steps). For each step describe:
- What changes are made
- How to verify correctness (tests, manual checks)
- Any migration or backwards-compatibility concerns

## Rules

- Do not ask for confirmation or clarifying questions. Register or update the
  issue directly. If anything is ambiguous, assume the obvious default and
  proceed.
- Do not write, edit, or commit any code — this only creates or updates the
  issue.
- Describe the work as a plan (what to do), not as a completed change.
- Write in the clarity and flow of Martin Kleppmann — engaging, classic style,
  smooth transitions between sections.
- Use callouts (blockquotes) for key concepts, definitions, and edge cases.
- Use ASCII diagrams (not images) when helpful.
- End issue bodies with:
  🤖 Generated with [Claude Code](https://claude.com/claude-code)
