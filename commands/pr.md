---
description: Push the current changes and open a detailed, explain-diff-style PR
allowed-tools: Read, Grep, Glob, Bash(git status:*), Bash(git branch:*), Bash(git checkout:*), Bash(git add:*), Bash(git commit:*), Bash(git push:*), Bash(git log:*), Bash(git diff:*), Bash(git show:*), Bash(gh pr create:*), Bash(gh pr view:*), Bash(gh repo view:*), Write
---

Optional title/notes: $ARGUMENTS

Take the current working-tree changes exactly as they are and open a pull
request with a **detailed but readable** body — the same depth and style as the
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
   `gh pr create --body-file <tempfile>`. Write the title and body **in Korean**,
   based on the real diff and commit history. If `$ARGUMENTS` is given, use it as
   the title or as extra context for the body.
6. Print the PR URL and stop.

## PR body structure

The body must contain these sections, in this order:

### 요약 (TL;DR)

The reviewer should grasp the whole change in ~15 seconds, before any
background. Write 3–4 lines (or a short bullet list) answering: **무엇을** 왜
바꿨는지, **어떻게** 바꿨는지, 그리고 **리뷰 시 주목할 곳**. A small table
(변경 전 / 변경 후) or a one-line summary of each key file works well. No deep
background here — just the essence.

### 배경 (Background)

Only the existing-system context a reviewer needs to make sense of this change.
Explore surrounding code, but keep it tight:
- A deeper background for newcomers — mark it as skippable if already familiar
- The narrower background directly relevant to this change
Cut context the reviewer won't use.

### 핵심 아이디어 (Intuition)

Explain the core intuition, essence first — not full details. Prefer a concrete
example with toy data over abstract prose. Use ASCII diagrams and tables where
they make the shape clearer.

### 변경 내용 (Code)

A high-level walkthrough of the changes, grouped and ordered so they're easy to
follow. Show key code snippets; skip the boilerplate. Point out anything the
reviewer should look at closely.

## Rules

- Do not ask for confirmation or clarifying questions. Push and open the PR
  directly. If anything is ambiguous, assume the obvious default and proceed.
- Ship the current changes as-is — never edit source files to polish the diff.
- If the working tree is clean and the branch is already pushed with no new
  commits vs. the base, say there is nothing to PR instead of creating an empty one.
- Never force-push, never target or push directly to the default branch.

### Readability (write to be understood fast)

- **Lead with the point (BLUF).** Every section opens with its key sentence;
  supporting detail follows.
- **Short paragraphs, one idea each** — aim for 3–4 sentences, not walls of text.
- **Plain language over jargon.** When a technical term is unavoidable, gloss it
  in one line the first time it appears. Write to be understood, not to impress.
- **Concise, not exhaustive.** Include what a reviewer needs to review well; cut
  padding, restatement, and background they won't use.
- **Show, don't just tell.** A concrete example with toy data beats a paragraph
  of abstract explanation.
- **Make it scannable.** Use headings, bullets, tables, and ASCII diagrams (not
  images) so a reviewer can skim structure before reading prose.
- Use callouts (blockquotes) for key concepts, definitions, and edge cases.
- Aim for the clarity and flow of Martin Kleppmann — approachable and
  well-connected, never verbose or stiff.
- End PR bodies with:
  🤖 Generated with [Claude Code](https://claude.com/claude-code)
