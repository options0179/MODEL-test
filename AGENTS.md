# AGENTS.md

이 파일은 작업 규칙의 위치만 안내한다. 또한, 코드작성을 제외한 모든 작업은 `MMNN-`앞에 날짜 포함하고, `.gitignore`에 최상위폴더를 기입한다는 절대적 추가규칙이 포함된다.
모든 규칙 문서를 한 번에 읽지 말고, 현재 작업 단계에 필요한 문서만 `agent-workflow-bundle` 폴더안에서 선택해서 읽는다.

## 문서 선택

| 현재 상황 | 읽을 문서 | 이유 |
|---|---|---|
| 작업을 처음 받고 범위·문서·계획 구조를 파악할 때 | `WORKFLOW.md` | 사용자 요구, `PROMPT.md`, `PLAN.md`, `TASK.md`, `TEST.md`, `HANDOFF.md`, `FAIL.md`의 역할과 읽는 순서가 정의되어 있다. |
| 구현 계획을 나누거나 실제 코드를 작성·테스트할 때 | `DEVELOPMENT.md` | Head/Worker 역할, Domain·Phase 분할, 최소 탐색, 병렬 작업, 반복 실패 처리 기준이 정의되어 있다. |
| Phase 또는 전체 작업을 끝내고 병합·통합 검증·결과 반환할 때 | `COMPLETION.md` | 작업 종료 순서, 병합 전 확인, 최종 검증, 사용자 반환 형식이 정의되어 있다. |
| branch, worktree, commit, merge 등 Git 작업을 수행할 때 | `GIT-MANAGEMENT.md` | Git 작업 범위, 커밋 메시지, 병렬 작업 격리, 위험 명령 제한이 정의되어 있다. |

## 읽기 원칙

- 현재 사용자 요구를 먼저 확인한다.
- `PROMPT.md`와 현재 요구를 대조한다.
- 현재 단계에 필요한 규칙 문서만 읽는다.
- 관련 없는 `docs-*`, 다른 Domain의 완료된 `TASK.md`, 다른 Phase의 `TEST.md`를 선제적으로 읽지 않는다.
- 작업 단계가 바뀔 때 필요한 규칙 문서를 추가로 읽는다.

## 플러그인 스킬 호출

이 저장소의 재사용 가능한 작업 규칙은 `261016-01-agent-workflow-plugin/`의 `agent-workflow-rules` 플러그인으로 제공한다. 플러그인이 설치된 환경에서는 다음 스킬을 명시적으로 호출한다.

| 작업 상황 | 호출할 스킬 |
|---|---|
| 작업 시작·범위·문서 선택 | `$workflow-start` |
| 계획 분할·구현·테스트 | `$development-execution` |
| Phase 완료·통합 검증·결과 반환 | `$completion-handoff` |
| branch·worktree·commit·merge | `$git-management` |
| 코드 변경 후 결과 출력 | `$output-summary` |

코드 또는 설정을 변경한 뒤에는 최종 응답 전에 `$output-summary`를 호출하고, 반드시 다음 형식으로 결과를 반환한다.

```text
## 한 일
- 실제로 완료한 변경

## 하지 않은 일 (그 이유)
- 수행하지 않은 항목과 구체적인 이유

## 실패한 일 (그 이유)
- 시도했지만 실패한 작업과 확인된 실패 원인

## 검증 결과
- 실행한 검증과 결과
```

플러그인이 설치되지 않은 환경에서는 동일 플러그인 폴더의 해당 `SKILL.md`를 직접 읽어 같은 규칙을 적용한다.
