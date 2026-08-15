---
description: Push the current changes and open a PR — summary first, plain and easy to read
allowed-tools: Read, Grep, Glob, Bash(git status:*), Bash(git branch:*), Bash(git checkout:*), Bash(git add:*), Bash(git commit:*), Bash(git push:*), Bash(git log:*), Bash(git diff:*), Bash(git show:*), Bash(gh pr create:*), Bash(gh pr view:*), Bash(gh repo view:*), Write
---

Optional title/notes: $ARGUMENTS

Take the current working-tree changes exactly as they are and open a pull
request. Lead with a short summary, then add only as much detail as the change
needs. Do not refactor, clean up, or "improve" the diff first.

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

## 본문 구조

정해진 섹션을 채우는 게 아니라, **요약을 맨 위에 두고 그 아래에 필요한 만큼만**
세부 내용을 적는다.

1. 맨 위에 **요약**. 배경 설명보다 먼저, 3~4줄(또는 짧은 목록)로 핵심만:
   무엇을 왜 바꿨는지 · 어떻게 바꿨는지 · 리뷰할 때 어디를 주목할지. 바쁜
   리뷰어가 요약만 읽어도 전체가 잡히게. (변경 전 / 변경 후 표나, 핵심
   파일별 한 줄 요약도 좋다.)
2. 그 아래에 **세부 내용**을 필요한 만큼만 이어 적는다. 다룰 만한 것: 이
   변경을 이해하는 데 필요한 기존 동작(배경), 왜 이렇게 풀었는지(핵심
   생각), 실제로 바뀐 코드를 이해하기 쉬운 순서로 훑기. 변경이 작으면 짧게,
   크면 자세히 — 필요 없는 부분은 그냥 생략한다. 정해진 섹션 수를 채우려
   하지 말 것.

핵심 코드 조각만 보여주고 뻔한 부분은 건너뛴다. 리뷰어가 특히 눈여겨봐야 할
곳은 짚어 준다. 말보다 예시가 낫다: 간단한 예시 데이터와, 구조가 한눈에
보이는 (그림 대신) 아스키 그림·표를 쓴다.

## Rules

- Do not ask for confirmation or clarifying questions. Push and open the PR
  directly. If anything is ambiguous, assume the obvious default and proceed.
- Ship the current changes as-is — never edit source files to polish the diff.
- If the working tree is clean and the branch is already pushed with no new
  commits vs. the base, say there is nothing to PR instead of creating an empty one.
- Never force-push, never target or push directly to the default branch.

### 쉽게 쓰기 (읽자마자 이해되게)

- **요약을 맨 앞에.** 각 부분은 핵심 문장으로 시작하고 부연은 뒤에 붙인다.
- **쉬운 단어로.** 처음 보는 어려운 말 대신 누구나 아는 쉬운 말을 쓴다.
  잘 보이려 어렵게 쓰지 말 것.
- **영어 대신 한글.** 영어 약어·외래어(TL;DR, BLUF 등)를 쓰지 말고 한글로
  풀어 쓴다. 코드에 실제 쓰이는 이름이나, 한글로 옮기면 오히려 헷갈리는
  기술 용어만 예외로 영어를 쓰되, 처음 나올 때 한 줄로 뜻을 덧붙인다.
- **짧게.** 리뷰에 필요한 것만 적고 군더더기·반복·안 쓸 배경은 뺀다. 한
  문단에는 한 가지 생각만, 3~4문장 안쪽으로.
- **보여주기.** 추상적인 설명보다 간단한 예시 데이터가 낫다.
- **훑어보기 좋게.** 제목·글머리표·표·(그림 대신) 아스키 그림으로 구조가
  한눈에 보이게 한다.
- 중요한 개념·정의·주의점은 인용문(>)으로 표시한다.
- PR 본문 끝에는 다음을 붙인다:
  🤖 Generated with [Claude Code](https://claude.com/claude-code)
