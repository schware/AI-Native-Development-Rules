# 01. AI Native SDLC

## 1. 이 문서가 생긴 대화의 흐름

처음에는 기존 SDLC에 AI 코딩 단계를 추가하면 된다고 생각했다.

```text
Requirement
→ Design
→ Code
→ Test
→ Deploy
```

그러나 대화를 통해 다음 문제가 드러났다.

- AI가 빠르게 코딩해도 문제와 설계가 틀리면 잘못된 결과가 더 빨리 늘어난다.
- 하나의 Agent가 분석, 설계, 구현과 검증을 모두 하면 책임과 Context가 섞인다.
- 사람이 모든 AI 산출물을 동일하게 검토하면 승인 병목이 된다.
- AI가 Vision과 Decision을 작성하고 사람이 통과만 시키면 실제 결정자는 AI가 된다.
- 운영 결과를 지식으로 환류하지 않으면 문서와 실제 시스템이 분리된다.

그래서 AI Native SDLC는 코드 생성 절차가 아니라 인간 결정, Agent 실행, 독립 검증과 지식 갱신을 포함하는 생명주기로 발전했다.

## 2. 목적

00에서 검증된 문제를 설계, 구현, 검증, 릴리스, 운영과 학습이 가능한 시스템으로 전환한다.

## 3. 10단계 생명주기

다음 10단계는 합치지 않는다.

```text
Vision
→ Specification
→ Domain Modeling
→ Architecture
→ Planning
→ Implementation
→ Verification
→ Release
→ Operation
→ Learning
```

10단계는 10개의 Agent나 회의를 뜻하지 않는다. 각 단계의 목적과 책임을 구분한다는 뜻이다.

## 4. 단계별 계약

```yaml
stage:
  id:
  purpose:
  inputs:
  outputs:
  proposer:
  consulted:
  reviewer:
  decision_owner:
  recorder:
  validation:
  risk_level:
  next_gate:
```

## 5. 사람과 AI의 역할

### AI

- 질문과 선택지를 만든다.
- 근거와 트레이드오프를 분석한다.
- 추천안을 제시한다.
- 구현과 반복 검증을 수행한다.
- 사람이 선택한 결과를 기록한다.

### 사람과 역할

- 해결할 문제와 우선순위를 선택한다.
- 위험을 수용한다.
- 중요한 기술, 보안과 출시 결정을 내린다.
- AI 추천을 통과시키는 것이 아니라 선택지 중 하나를 직접 고른다.

## 6. 역할 기반 결정권

사람 이름보다 역할을 기준으로 정의한다.

```yaml
decision_authority:
  vision:
    decision_owner: product_owner
  architecture:
    decision_owner: tech_lead
  security:
    decision_owner: security_reviewer
  release:
    decision_owner: release_manager
```

1인 프로젝트에서는 한 사람이 여러 역할을 겸하지만 결정 이력에는 역할을 분리해서 기록한다.

## 7. 위험 등급과 검토 깊이

### 경량

문구, 스타일, 테스트 추가, 동작을 바꾸지 않는 리팩터링

```text
자동 테스트와 lint 중심
```

### 표준

기존 구조 안에서 기능을 추가하거나 변경하는 작업

```text
별도 AI Session 리뷰
→ 작성자 확인
```

### 고위험

다음 질문 중 하나라도 예이면 고위험 후보다.

1. 되돌리기 어려운가
2. 영향 범위가 넓은가
3. 사용자, 돈, 보안에 영향을 주는가

대표 항목:

- DB 스키마와 데이터 마이그레이션
- 데이터 삭제와 개인정보
- 인증과 권한
- 공개 API 계약
- 유료 서비스와 인프라 비용
- 운영 배포
- 서비스 경계와 핵심 기술 선택
- Agent 권한 변경

```text
독립 AI 리뷰
→ 작성자가 아닌 역할의 승인
```

1인 프로젝트에서는 새로운 Session, 시간 간격과 고위험 체크리스트를 최소 통제로 사용한다.

## 8. 독립 검증

같은 Session의 AI는 구현 이유와 가정을 알고 있어 같은 착각을 반복할 수 있다. 독립 Reviewer에게는 기본적으로 다음만 제공한다.

```text
Diff
수용 기준
관련 계약
테스트 결과
필수 안전 Context
```

검증 Agent와 구현 Agent가 충돌하면 Decision Owner가 판단한다.

## 9. 같은 PR에서 상태 갱신

가능한 한 다음을 같은 PR에서 검토한다.

```text
코드
테스트
관계 메타데이터
Current State Patch
필요한 사람용 문서
```

같은 PR은 같은 작성자가 모든 결정을 내린다는 뜻이 아니다. 위험에 따라 다른 역할의 승인을 요구한다.

## 10. 개발자의 착각과 실패 패턴

- AI 코딩 속도를 프로젝트 전체 속도로 착각한다.
- 설계가 부족해도 AI가 좋은 구조를 만든다고 생각한다.
- 테스트 통과를 사용자 가치와 운영 안전의 증명으로 본다.
- Agent 수가 많으면 품질이 자동으로 오른다고 생각한다.
- 사람의 승인 버튼을 인간 결정으로 착각한다.
- 모든 산출물을 같은 깊이로 읽어야 안전하다고 생각한다.

주요 실패 모드:

```text
Problem Drift
Scope Drift
Context Drift
State Drift
Architecture Drift
Knowledge Drift
질문 피로
승인 병목
책임 불명확
자기검증 편향
```

## 11. 현재 합의와 미해결 사항

### 합의

- 10단계를 유지한다.
- Decision Owner는 역할로 정의한다.
- 위험 등급에 따라 검토 깊이를 달리한다.
- 표준과 고위험 작업은 별도 Reviewer Session을 사용한다.
- 코드와 관련 상태 변경은 같은 PR에서 검토한다.

### 미해결

- Vision, 제품, 기술, 보안 결정 간 충돌 해결 역할
- 위험 등급 하향 승인 절차
- 1인 프로젝트의 고위험 대체 통제
- 단계별 최소 산출물과 Gate

## 12. 앞으로의 비전

01은 AI 자동화 파이프라인이 아니라 사람이 실제 결정권을 갖고 AI가 제안, 실행과 기록을 맡는 개발 운영 체계로 발전한다. 성공 기준은 코드 생성량이 아니라 재작업 감소, 위험 발견, 결정 추적성과 운영 학습이다.

---

# 참고 문서

- [Atlassian Product Discovery 소개](https://www.atlassian.com/agile/product-management/discovery)
- [Jira Product Discovery 공식 가이드](https://www.atlassian.com/software/jira/product-discovery/guides/getting-started/introduction)
- [Anthropic, Building Effective Agents](https://www.anthropic.com/engineering/building-effective-agents)
- [Anthropic, Effective Context Engineering for AI Agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)
- [OpenAI, A Practical Guide to Building AI Agents](https://openai.com/business/guides-and-resources/a-practical-guide-to-building-ai-agents/)
- [OpenAI, Building Agents 학습 경로](https://developers.openai.com/tracks/building-agents)
- [Microsoft Azure Well-Architected, ADR 유지 관리](https://learn.microsoft.com/ko-kr/azure/well-architected/architect-role/architecture-decision-record)
- [Architecture Decision Record 자료 저장소](https://github.com/architecture-decision-record/architecture-decision-record)
- [Backstage Software Catalog](https://backstage.io/docs/features/software-catalog/)
- [Model Context Protocol 소개](https://modelcontextprotocol.io/docs/2026-07-28/getting-started/intro)
- [Model Context Protocol 아키텍처](https://modelcontextprotocol.io/docs/2026-07-28/learn/architecture)
