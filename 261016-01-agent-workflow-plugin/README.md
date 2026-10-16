# Agent Workflow Rules

`AGENTS.md`가 가리키는 `agent-workflow-bundle`의 작업 규칙을 재사용 가능한 Cowork 플러그인 스킬로 분리한 플러그인이다.

## 포함된 스킬

- `workflow-start`: 작업 시작, 범위 확인, 필요한 문서 선택
- `development-execution`: Domain/Phase 분할, Agent 실행, 테스트, 반복 실패 처리
- `completion-handoff`: Phase 완료, 병합 전 확인, 통합 검증, 결과 반환
- `git-management`: branch/worktree, commit, merge, 금지 명령
- `output-summary`: 코드 변경 후 `한 일 / 하지 않은 일 (그 이유) / 실패한 일 (그 이유) / 검증 결과` 형식의 결과 출력

원본 문서는 저장소의 `agent-workflow-bundle/`에 보존한다. 이 플러그인은 원본을 변경하지 않으며, 각 스킬을 필요한 작업에서만 온디맨드로 사용하도록 구성되어 있다.
