---
name: completion-handoff
description: >
  This skill should be used when a phase or task is complete, when reviewing
  handoffs or failures before merge, when running integration verification, or
  when preparing the final result for the user.
metadata:
  version: "0.1.0"
---

# 완료·병합·결과 반환

## Worker 종료 조건

Worker는 다음 상태까지 만든다.

```text
코드 수정 → Phase 테스트 → 변경사항 검토 → Commit → 병합 가능 여부 확인
```

다른 Domain의 코드와 충돌하면 임의로 재작성하지 않고 Head Agent에게 반환한다.

## Head Agent 마무리

모든 Worker 결과를 확인한 뒤 다음 순서를 따른다.

```text
Phase 결과 확인 → HANDOFF/FAIL 확인 → 필요한 병합 → 통합 테스트 → PLAN 상태 정리 → 남은 문제 확인 → 결과 반환
```

완료 내용을 별도 결과 문서에 다시 복사하지 않는다. 진행 상태는 `PLAN.md`, 구현 범위는 `TASK.md`, 검증 결과는 `TEST.md`, Domain 간 요청은 `HANDOFF.md`, 반복 실패는 `FAIL.md`에 둔다.

## 사용자 결과 반환

완료된 경우 다음만 간결하게 요약한다.

- 수행한 작업
- 변경된 영역
- 검증 결과
- 남은 문제

해결하지 못한 문제가 있으면 막힌 작업, 막힌 원인, 확인된 상태, 사용자가 결정해야 하는 사항을 구분해 반환한다. 기존 문서를 그대로 반복하지 말고 결과 판단에 필요한 내용만 요약한다.

코드 또는 설정 변경이 포함된 작업은 최종 응답 전에 `$output-summary`를 호출한다. 출력은 `한 일`, `하지 않은 일 (그 이유)`, `실패한 일 (그 이유)`, `검증 결과` 순서를 지킨다.
