# 08. AI Native Agent Organization

## 1. 이 문서가 생긴 대화의 흐름

Workflow를 정의하자 각 단계의 일을 누가 하는지 질문이 생겼다. 하나의 Agent가 상담, 문서화, DDD, 설계, 코딩, 테스트, 배포와 운영을 모두 수행하면 Context와 책임이 섞인다.

그래서 Agent 수를 늘리는 것이 아니라 먼저 업무 경계와 책임을 정의해야 한다는 결론에 도달했다.

또한 팀을 기준으로 생각하자 다음 문제가 추가되었다.

- 승인자를 특정 사람 이름으로 정하면 확장되지 않는다.
- 여러 사람이 각자의 AI로 같은 상태 파일을 수정하면 충돌한다.
- 사람 사이의 제품, 기술과 보안 결정권도 정해야 한다.
- 구현 Agent가 자신의 결과를 검토하면 같은 착각을 반복할 수 있다.
- 모든 AI 산출물을 사람이 전부 읽으면 승인 병목이 된다.

이 문제가 08을 단순 Agent 목록이 아니라 사람과 Agent의 운영 모델로 만들었다.

## 2. 목적

Agent의 역할, 책임, 입력, 출력, 권한, Context, 결정권, 승인과 중단 조건을 계약으로 정의한다.

## 3. 기본 원칙

```text
예측 가능한 절차
→ 일반 코드 또는 Workflow

판단과 불확실성이 필요한 업무
→ Agent
```

단일 Agent로 충분하면 Multi-Agent를 만들지 않는다.

## 4. 역할 체계

### Discovery

문제 후보, 가설과 검증 계획

### Question / Consultation

작은 질문, 선택지와 쉬운 설명

### Documentation

대화와 사람의 결정을 검토 가능한 문서로 변환

### DDD

공통 언어, Domain, Bounded Context와 관계

### Architecture

기술 대안, 비기능 요구와 ADR 초안

### Planning

Epic, Story, Task와 수용 기준

### Coding

승인된 범위의 코드, 테스트와 PR

### QA

독립 테스트, 회귀, 보안과 요구사항 검증

### Deployment

승인된 릴리스 배포와 롤백 정보

### Operations

지표, 로그, 비용과 인시던트 분석

### Knowledge

Current State, 분산 관계, 색인과 Graph 갱신 후보

### Orchestrator

라우팅, Context Budget, 권한, 승인과 중단 관리

## 5. Agent 계약

```yaml
agent:
  id:
  purpose:
  inputs:
  outputs:
  tools:
  permissions:
  context_budget:
  proposed_decisions:
  prohibited_decisions:
  approval:
  stop_conditions:
  evaluation:
```

## 6. AI 제안과 사람 결정

```text
AI가 선택지, 근거, 트레이드오프와 추천 제시
→ Decision Owner 역할이 실제 선택
→ AI가 선택 결과와 근거 기록
```

AI가 Vision이나 Decision을 작성하고 사람이 승인만 하면 실제 결정자는 AI가 된다. 따라서 Agent의 `may`와 `may_not`을 명확히 한다.

```yaml
architecture_agent:
  may:
    - analyze_options
    - recommend_option
    - draft_adr
  may_not:
    - accept_architecture_decision
    - accept_security_risk
    - approve_production_release
```

## 7. 역할 기반 결정권

```yaml
vision_decision:
  proposer:
    - discovery_role
    - product_owner
  consulted:
    - tech_lead
    - design_role
  decision_owner: product_owner
  recorder: documentation_agent
  challengers:
    - any_team_member
```

한 사람이 여러 역할을 겸할 수 있지만 역할별 결정 이력은 남긴다.

## 8. 독립 Reviewer Session

작성 Agent와 Reviewer Agent의 Context를 분리한다.

Reviewer에게는 기본적으로 다음만 제공한다.

```text
Diff
수용 기준
관련 계약
테스트 결과
필수 안전 Context
```

등급별 처리:

```text
경량 = 자동 검사
표준 = 별도 AI Session 리뷰 + 작성자 확인
고위험 = 별도 AI Session 리뷰 + 작성자가 아닌 역할 승인
```

## 9. 사용자 접근성

사용자는 내부 Agent 조직을 알 필요가 없다.

```text
사용자
→ 하나의 상담 인터페이스
→ Orchestrator와 전문 역할
→ 쉬운 설명과 중요한 승인 요청
→ 사용자
```

전문 용어는 숨기는 것이 아니라 필요한 순간에 번역한다.

## 10. 소규모 팀 MVP

처음에는 다음 네 논리적 역할로 시작한다.

```text
Discovery / Consultation
Builder
Reviewer
Knowledge
```

한 모델이 여러 역할을 맡더라도 Session, 권한과 Context는 분리한다.

## 11. 개발자의 착각과 실패 패턴

- Agent 수가 많으면 품질이 높아진다고 생각한다.
- 역할 이름만 정하면 책임 경계도 자동으로 생긴다고 생각한다.
- AI의 승인 요청이 충분한 Human-in-the-Loop라고 생각한다.
- 작성 Agent가 자신을 검토해도 독립된 검증이라고 생각한다.
- Knowledge Agent가 상태를 직접 확정해도 된다고 생각한다.
- 한 사람에게 모든 권한이 있어도 역할 기록이 필요 없다고 생각한다.

주요 실패:

```text
역할 중복
Context 복제
무한 위임
자기검증 편향
과도한 권한
비용 폭증
Agent 간 가정 충돌
결정권 충돌
```

## 12. 현재 합의와 미해결 사항

### 합의

- 역할과 권한을 먼저 정의한다.
- AI 추천과 사람 결정을 분리한다.
- Decision Owner는 역할로 지정한다.
- 수행자와 검증자를 가능한 한 분리한다.
- 고위험 작업은 다른 역할이 승인한다.
- 소규모 팀은 네 역할 MVP로 시작한다.

### 미해결

- 제품, 기술, 보안, 배포 결정 간 충돌 해결 규칙
- Multi-Agent 전환 임계 조건
- 1인 팀의 고위험 대체 검증
- Orchestrator 권한과 중단 규칙
- Agent 간 Context 전달의 최소 형식

## 13. 앞으로의 비전

08은 코딩 Agent들의 목록이 아니라 사람과 Agent의 책임, 결정권과 독립 검증을 정의하는 운영 모델로 발전한다. 장기적으로는 팀원이 각자의 AI를 사용하더라도 동일 Source of Truth와 정책 아래 협업하고, 역할과 위험에 따라 자동화 수준을 조절할 수 있어야 한다.

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
