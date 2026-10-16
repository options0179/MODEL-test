---
name: workflow-start
description: >
  This skill should be used when starting a task, checking AGENTS.md,
  comparing a request with PROMPT.md, deciding which workflow documents to
  read, or resolving a scope conflict before implementation.
metadata:
  version: "0.1.0"
---

# 작업 시작과 범위 확인

현재 사용자 요구를 먼저 확인하고, 저장소의 `AGENTS.md`가 지정한 규칙을 따른다.

## 시작 순서

1. 현재 사용자 요구를 읽는다.
2. `PROMPT.md`가 있으면 목적, 범위, 제약, 완료 기준과 대조한다.
3. 판단에 필요한 기존 코드와 문서만 최소 탐색한다.
4. 기존 `PLAN.md`가 있으면 확인하고, 없으면 작업이 복잡한 경우에만 계획 작성을 고려한다.
5. 계획이 실행 가능하고 사용자 요구와 충돌하지 않을 때만 다음 단계로 이동한다.

`PROMPT.md`가 없으면 없는 사실을 보완해 만들지 말고, 현재 사용자 요구를 기준으로 범위를 기록한다.

## 문서 선택

- 작업을 처음 받고 범위와 문서 구조를 파악할 때 `WORKFLOW.md`를 읽는다.
- 계획을 나누거나 구현·테스트할 때 `DEVELOPMENT.md`를 읽는다.
- Phase 또는 전체 작업을 끝내고 통합 검증과 결과 반환을 할 때 `COMPLETION.md`를 읽는다.
- branch, worktree, commit, merge를 다룰 때 `GIT-MANAGEMENT.md`를 읽는다.
- 현재 판단에 필요하지 않은 다른 Domain의 `TASK.md`, `TEST.md`, `HANDOFF.md`, `FAIL.md`, 관련 없는 `docs-*`는 읽지 않는다.

## 문서 책임

- `PROMPT.md`: 작업 목적, 범위, 제약, 완료 기준
- `docs-*`: 반복 참조할 설명, 조사 결과, 기준, 기술 선택 근거
- `PLAN.md`: 전체 순서, Domain/Phase, 의존 관계, 진행 상태
- `TASK.md`: 해당 Phase의 실제 작업 범위와 완료 조건
- `TEST.md`: 검증 기준과 결과
- `HANDOFF.md`: 다른 Domain 또는 Agent에 실제로 요청할 내용
- `FAIL.md`: 같은 작업 또는 검증이 두 번 연속 실패했을 때의 원인 기록

같은 내용을 여러 문서에 반복해서 작성하지 않는다. 사용자 요구가 기존 범위와 충돌하면 임의로 강행하지 말고, 충돌 지점과 필요한 판단을 먼저 제시한다.
