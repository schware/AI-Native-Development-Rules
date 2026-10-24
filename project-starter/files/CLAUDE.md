# 이 프로젝트의 AI 작업 규칙

이 프로젝트는 AI Native Development Rules를 따른다.

- 공통 규칙은 `.framework/specification/`에 있다. `.framework/`는 Rules 저장소를 가리키는 submodule이며, `project.yaml`의 `git_ref` 버전을 가리킨다(00.common §11.5).
- 이 프로젝트에만 적용하는 규칙은 `current-state.md`에 있다.
- `.framework/`가 비어 있으면 작업을 시작하지 말고, 사람에게 `git submodule update --init` 실행을 요청한다.

## 작업 전에 읽을 것 (00.common §12.2)

1. `project.yaml`
2. `.framework/specification/00.common/README.md`
3. `.framework/specification/07.decision/README.md`
4. `current-state.md`
5. 작업과 관련된 `records/`의 기록

## 반드시 지킬 것

- 명세의 "검토 중인 항목"은 따르지 않는다.
- 결과만 요청받으면 바로 만들지 않는다. 목적, 조건, 사람이 골라야 할 선택을 먼저 확인한다 (00.common §5.4).
- 설명을 요청받으면 "어떻게 동작하는가"와 "왜 그렇게 만들었는가"를 함께 설명한다.
- `.framework/` 안의 파일은 고치지 않는다. 공통 규칙을 바꿀 필요가 있으면 그 내용과 이유를 사람에게 보고한다. 반영은 사람이 Rules 저장소에 요청한다.
- 이 프로젝트에만 적용할 규칙이 필요하면 결정 후보(`proposed`)를 작성하고 결정을 요청한다. 결정되면 `current-state.md`에 결정 ID와 함께 적는다.
- 결정의 `status`를 `decided` 또는 `rejected`로 바꾸지 않는다. 결정은 사람만 한다.
- `decided_by`와 `confirmed_by`에 AI를 적지 않는다.
- 내가 쓴 내용은 `drafted_by`를 `ai_agent` 또는 `mixed`로 적는다.
- 과거 결정을 근거로 말할 때는 결정 ID를 함께 제시한다. ID가 없으면 결정이 아니다.
- `current-state.md`와 다른 기술이나 구조로 바꿔야 하면, 구현을 멈추고 결정 후보(`proposed`)를 먼저 작성한다.
- 규칙이 충돌하면 임의로 해석하지 않고 멈춘 뒤 보고한다 (00.common §5.3).
- 커밋 메시지에는 관련 기록 ID를 `Record-Refs`로 적는다 (00.common §8.5).
- commit과 push는 사람이 요청할 때만 한다.
