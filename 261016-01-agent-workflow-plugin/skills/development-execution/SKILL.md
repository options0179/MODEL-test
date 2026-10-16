---
name: development-execution
description: >
  This skill should be used when dividing implementation work into domains or
  phases, assigning worker tasks, writing code, running phase tests, or handling
  repeated implementation failures.
metadata:
  version: "0.1.0"
---

# 구현 계획과 실행

작업을 현재 사용자 요구와 기존 범위 안에서 최소 변경으로 나눈다. 새 구조를 만들기 전에 기존 코드로 해결할 수 있는지 확인한다.

## Head Agent

다음 순서로 판단한다.

```text
사용자 요구 확인 → PROMPT.md 대조 → 관련 코드 최소 탐색 → 필요한 docs 확인 → 변경 범위 결정
```

Domain은 비즈니스 책임, 코드 수정 범위, 충돌 가능성, 독립 검증 가능성을 기준으로 나눈다. 각 Domain의 Phase는 명확한 목적과 검증 가능한 완료 조건을 가져야 하며, `PLAN.md`에는 목적과 의존 관계만 기록한다. 상세 구현은 `TASK.md`에 둔다.

## 병렬 작업

다음 조건을 모두 만족할 때만 Phase를 병렬로 수행한다.

- 수정 범위가 크게 겹치지 않는다.
- 직접적인 선행 의존성이 없다.
- 각 작업을 독립적으로 검증할 수 있다.

다른 Domain의 결과가 필요하면 임의로 수정하지 말고 `HANDOFF.md`로 요청한다.

## Worker Agent

할당된 `TASK.md` 범위만 수행한다.

```text
TASK 확인 → 관련 코드 최소 탐색 → 최소 계획 → 코드 작성 → 관련 테스트 → 변경 검토 → 병합 가능 여부 확인
```

범위를 벗어나는 변경은 하지 않는다. 다른 Domain 수정이 필요하면 `HANDOFF.md`로 반환한다.

## 최소 탐색과 검증

한 번에 관련 파일, 직접 의존 코드, 정확한 심볼 또는 문자열, 관련 테스트와 필요한 문서만 확인한다. 판단이 가능해지면 추가 탐색을 중단한다.

코드 변경 후에는 정적 오류를 확인하고, 직접 변경한 영역의 관련 테스트를 우선 실행한다. 전체 통합 테스트는 Head Agent가 필요할 때 수행한다.

## 반복 실패

첫 실패는 원인을 확인하고 수정한 뒤 재시도한다. 같은 작업이 두 번째로 실패하면 `FAIL.md`에 실패 단계, Domain, 현상과 추정 원인을 기록하고 같은 접근을 중단한 뒤 재계획한다.
