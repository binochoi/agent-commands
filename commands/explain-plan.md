---
description: Explain a plan, proposal, or design document — saves to .explain-codes/plan/
allowed-tools: Read, Grep, Glob, Bash(git log:*), Bash(git diff:*), Bash(gh pr view:*), WebFetch, Write
---

Target: $ARGUMENTS

Explain the specified plan, proposal, design doc, or RFC. The argument is a file path, PR URL, issue URL, or free-text description.

Write the explanation to `.explain-codes/plan/YYYY-MM-DD-<slug>.md` (relative to repo root), where `<slug>` is a short kebab-case identifier derived from the target. Create the directory if it does not exist.

The file must contain these sections:

## Context

Describe the problem this plan addresses. What is broken, missing, or suboptimal? What prior solutions or discussions exist in the codebase (issues, prior PRs, TODO comments)? Include both high-level business context and technical context.

## Design

Explain the proposed solution. Cover:
- Core idea and key design decisions
- Trade-offs (what was considered and rejected, and why)
- Data model, API surface, or component architecture — whichever is relevant
Use ASCII diagrams and tables liberally.

## Implementation Plan

Break the work into ordered steps. For each step describe:
- What changes are made
- How to verify correctness (tests, manual checks)
- Any migration or backwards-compatibility concerns

## Quiz

Create exactly five multiple-choice questions that test understanding of this plan. Medium difficulty — requires understanding the substance, but no gotchas. Present each question with options. After all five, provide the answers with brief explanations.

## Rules

- Do not ask clarifying questions. If the target is ambiguous, assume the reader wants a general explainer for the concept named.
- Do not produce HTML. Write everything as plain markdown to the file path above.
- Write in the clarity and flow of Martin Kleppmann — engaging, classic style, smooth transitions between sections.
- Use callouts (blockquotes) for key concepts, definitions, and edge cases.
- Use ASCII diagrams (not images) when helpful.
- Start the file with a title line `# <target>: <one-sentence summary>`.
- Answer in Korean.
