---
name: git-management
description: >
  This skill should be used when creating or switching branches or worktrees,
  preparing commits, merging work, checking Git state, or deciding whether a
  Git command is allowed under the repository workflow.
metadata:
  version: "0.1.0"
---

# Git 작업 관리

Git은 실제 코드 변경과 완료된 작업 단위를 기록하는 데 사용한다. `PLAN.md`와 `TASK.md`의 작업 구조를 Git 기록에 중복해서 쓰지 않는다.

## 시작과 격리

코드 수정 전 `git branch --show-current`와 `git status`를 확인한다. `main`에서 직접 작업하지 않는다. 병렬 작업은 작업별 branch와 worktree를 분리한다.

```text
1 Agent = 1 작업 범위 = 1 branch = 1 worktree
```

## Commit

Commit 전 `git status`와 `git diff`를 확인한다. 현재 작업과 관련된 변경만 stage하고, 하나의 Commit에는 하나의 의미 있는 변경만 포함한다.

메시지는 다음 형식의 한국어 한 줄로 작성한다.

```text
<타입>: <변경 대상> <변경 내용>
```

타입은 `feature`, `fix`, `refactor`, `test`, `docs`, `config` 중에서 선택한다. Agent명, Phase, Issue 번호, 진행 상태, `작업 완료`처럼 내용을 알 수 없는 표현은 넣지 않는다.

## Merge

`TASK` 완료와 `TEST` 통과를 확인하고, 충돌을 점검한 뒤 병합한다. 병합 후 통합 테스트를 실행한다. 다른 Agent의 branch, worktree, 작업 범위를 임의로 수정하지 않는다.

## 금지 명령

사용자 승인 없이 다음 명령을 실행하지 않는다.

```text
git push --force
git reset --hard
git clean -fd
git rebase
git branch -D
git worktree remove --force
```
