---
id: EXAMPLE001-D001
title: "현재 규칙을 current-state.md에 둔다"

status: decided
risk_level: medium

created_at: "2026-10-22"
decided_at: "2026-10-22"

drafted_by: ai_agent
confirmed_by: "Sun&Moon"
confirmed_at: "2026-10-22"

proposed_by: ai_agent
adoption: as_proposed
decided_by: "Sun&Moon"
decision_steward: PL

replaces: []

issues: []
---

# 현재 규칙을 current-state.md에 둔다

## 결론

지금 유효한 규칙은 저장소 루트의 `current-state.md` 한 파일에 둔다. 규칙마다 근거가 된 결정 ID를 붙이고, 결정과 같은 Pull Request에서 함께 고친다.

## 배경

첫 결정이 `decided`가 되면 지금 유효한 규칙이 생긴다. 그런데 `07.decision` §8.10에는 현재 규칙의 저장 위치가 검토 중인 항목으로만 남아 있어 둘 곳이 없었다.

## 검토한 대안

| 대안 | 장점 | 단점 |
|---|---|---|
| `current-state.md` (선택) | 사람과 AI가 함께 읽음, 결정 ID로 근거 추적 | 결정과 함께 손으로 고쳐야 함 |
| `current_state.yaml` | AI가 읽기 쉬움 | 사람이 읽기 어려움 |
| 별도 파일 없이 `decided` 결정에서 계산 | 원본이 하나 | `07.decision` §8.7 "결정 기록과 현재 규칙은 다르다"와 맞지 않음 |

## 결정 이유

`07.decision` §8.7과 맞고, 사람과 AI가 함께 읽을 수 있다. 결정 ID가 붙어 있어 근거도 따라갈 수 있다.

## 근거와 참고자료

- `specification/07.decision/README.md` §8.7, §8.10 (v0.1.0)
- v03 `02-project-knowledge-graph-source-of-truth.md`의 Current State와 Decision History 분리

## 영향

- 이후 결정이 `current-state.md`를 바꾸면 같은 Pull Request에서 함께 고친다(Pull Request 템플릿의 체크 항목).
- AI 지침(`CLAUDE.md`)의 "작업 전에 읽을 것"에 `current-state.md`를 넣는다.

## 미해결 질문

- 프로젝트에서 써 본 뒤, `07.decision` §8.10의 "현재 규칙의 저장 위치"를 이 방식으로 확정할지

## 관련 기록

- (없음)
