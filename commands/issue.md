---
description: Register the plan as a GitHub issue — summary first, plain and easy to read
allowed-tools: Read, Grep, Glob, Bash(git status:*), Bash(git branch:*), Bash(git log:*), Bash(git diff:*), Bash(git remote:*), Bash(git rev-parse:*), Bash(gh issue create:*), Bash(gh issue edit:*), Bash(gh issue view:*), Bash(gh repo view:*), Bash(gh label list:*), Write
---

Plan/topic to register: $ARGUMENTS

Take the plan for the work to be done and register it as a GitHub issue on the
current repo. Lead with a short summary, then add only as much detail as the
work needs. This is about *upcoming work*, not existing changes — describe what
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
3. Produce an updated body in the same shape as below (요약 먼저, 세부는 그
   아래): keep what still applies, and fold in the current conversation plan
   (plus any extra guidance in `$ARGUMENTS`). Do not blindly discard existing
   content.
4. Write the updated body to a temp file and apply it with
   `gh issue edit <N> --body-file <tempfile>` (add `--title` only if the title
   should change). Keep the title and body **in Korean**.
5. Print the issue URL and stop.

## 본문 구조

정해진 섹션을 채우는 게 아니라, **요약을 맨 위에 두고 그 아래에 필요한 만큼만**
세부 내용을 적는다.

1. 맨 위에 **요약**. 배경 설명보다 먼저, 3~4줄(또는 짧은 목록)로 핵심만:
   무엇을 왜 바꾸는지 · 어떻게 풀지 · 어디가 바뀌는지. 바쁜 사람이 요약만
   읽어도 전체 그림이 잡히게. (문제 / 해결 / 바뀌는 곳 표도 좋다.)
2. 그 아래에 **세부 내용**을 필요한 만큼만 이어 적는다. 다룰 만한 것: 왜
   필요한지(배경), 어떻게 풀지(방법·설계와 고른 이유), 할 일 순서(여러
   단계면 체크리스트로). 변경이 작으면 짧게, 크면 자세히 — 필요 없는 부분은
   그냥 생략한다. 정해진 섹션 수를 채우려 하지 말 것.

말보다 예시가 낫다: 간단한 예시 데이터를 설계에 대입해 보여주면 좋다. 구조가
한눈에 보이도록 (그림 대신) 아스키 그림과 표를 쓴다.

## Rules

- Do not ask for confirmation or clarifying questions. Register or update the
  issue directly. If anything is ambiguous, assume the obvious default and
  proceed.
- Do not write, edit, or commit any code — this only creates or updates the
  issue.
- Describe the work as a plan (what to do), not as a completed change.

### 쉽게 쓰기 (읽자마자 이해되게)

- **요약을 맨 앞에.** 각 부분은 핵심 문장으로 시작하고 부연은 뒤에 붙인다.
- **쉬운 단어로.** 처음 보는 어려운 말 대신 누구나 아는 쉬운 말을 쓴다.
  잘 보이려 어렵게 쓰지 말 것.
- **영어 대신 한글.** 영어 약어·외래어(TL;DR, BLUF 등)를 쓰지 말고 한글로
  풀어 쓴다. 코드에 실제 쓰이는 이름이나, 한글로 옮기면 오히려 헷갈리는
  기술 용어만 예외로 영어를 쓰되, 처음 나올 때 한 줄로 뜻을 덧붙인다.
- **짧게.** 필요한 것만 적고 군더더기·반복·안 쓸 배경은 뺀다. 한 문단에는
  한 가지 생각만, 3~4문장 안쪽으로.
- **보여주기.** 추상적인 설명보다 간단한 예시 데이터가 낫다.
- **훑어보기 좋게.** 제목·글머리표·표·(그림 대신) 아스키 그림으로 구조가
  한눈에 보이게 한다.
- 중요한 개념·정의·주의점은 인용문(>)으로 표시한다.
- 이슈 본문 끝에는 다음을 붙인다:
  🤖 Generated with [Claude Code](https://claude.com/claude-code)
