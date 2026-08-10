---
description: Register the plan as a detailed, explain-plan-style GitHub issue
allowed-tools: Read, Grep, Glob, Bash(git status:*), Bash(git branch:*), Bash(git log:*), Bash(git diff:*), Bash(git remote:*), Bash(git rev-parse:*), Bash(gh issue create:*), Bash(gh issue edit:*), Bash(gh issue view:*), Bash(gh repo view:*), Bash(gh label list:*), Write
---

Plan/topic to register: $ARGUMENTS

Take the plan for the work to be done and register it as a GitHub issue on the
current repo, with a **detailed but readable** body — the same depth and style
as the `explain-plan` command, minus the quiz. This is about *upcoming work*,
not existing changes — describe what should be done, not a diff.

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
3. Produce an updated body using the same section structure below: keep what
   still applies, and fold in the current conversation plan (plus any extra
   guidance in `$ARGUMENTS`). Do not blindly discard existing content.
4. Write the updated body to a temp file and apply it with
   `gh issue edit <N> --body-file <tempfile>` (add `--title` only if the title
   should change). Keep the title and body **in Korean**.
5. Print the issue URL and stop.

## Issue body structure

The body must contain these sections, in this order:

### 요약 (TL;DR)

The busiest reader should get the whole picture in ~15 seconds, before any
background. Write 3–4 lines (or a short bullet list) answering: **무엇을** 왜
바꾸려 하는지, **어떻게** 풀지, 그리고 **영향 범위**(어디가 바뀌나). A small
table (문제 / 해결 / 영향 범위) works well here. No deep background — just the
essence.

### 배경 (Context)

Only what a reader needs to understand *why this plan exists*. Describe what is
broken, missing, or suboptimal, and any prior solutions or discussions in the
codebase (issues, prior PRs, TODO comments). Keep it tight — cut tangents. If
some context is optional for those already familiar, say so and let them skip.

### 설계 (Design)

Explain the proposed solution, essence first:
- Core idea and key design decisions
- Trade-offs (what was considered and rejected, and why)
- Data model, API surface, or component architecture — whichever is relevant
Prefer a concrete example (toy data walked through the design) over abstract
prose. Use ASCII diagrams and tables where they make the shape clearer.

### 구현 계획 (Implementation Plan)

Break the work into ordered steps (a checklist when there are multiple). For
each step, briefly: what changes, how to verify it (tests, manual checks), and
any migration or backwards-compatibility concern. Keep each step scannable.

## Rules

- Do not ask for confirmation or clarifying questions. Register or update the
  issue directly. If anything is ambiguous, assume the obvious default and
  proceed.
- Do not write, edit, or commit any code — this only creates or updates the
  issue.
- Describe the work as a plan (what to do), not as a completed change.

### Readability (write to be understood fast)

- **Lead with the point (BLUF).** Every section opens with its key sentence;
  supporting detail follows.
- **Short paragraphs, one idea each** — aim for 3–4 sentences, not walls of text.
- **Plain language over jargon.** When a technical term is unavoidable, gloss it
  in one line the first time it appears. Write to be understood, not to impress.
- **Concise, not exhaustive.** Include what a reader needs to act; cut padding,
  restatement, and background they won't use.
- **Show, don't just tell.** A concrete example with toy data beats a paragraph
  of abstract explanation.
- **Make it scannable.** Use headings, bullets, tables, and ASCII diagrams (not
  images) so a reader can skim structure before reading prose.
- Use callouts (blockquotes) for key concepts, definitions, and edge cases.
- Aim for the clarity and flow of Martin Kleppmann — approachable and
  well-connected, never verbose or stiff.
- End issue bodies with:
  🤖 Generated with [Claude Code](https://claude.com/claude-code)
