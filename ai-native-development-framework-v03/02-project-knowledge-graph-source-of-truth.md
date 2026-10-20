# 02. Project Knowledge Graph & Source of Truth

## 1. 이 문서가 생긴 대화의 흐름

처음에는 모든 결정과 문서를 GitHub에 모으면 Agent가 프로젝트를 이해할 수 있다고 생각했다. 그러나 ADR과 문서가 수백 개가 되면 GitHub도 창고가 되고, Agent는 현재 상태를 찾기 위해 많은 문서를 읽어야 했다.

여기서 다음 전환이 일어났다.

```text
ADR = 현재 상태
```

가 아니라,

```text
ADR = 결정 이력
Current State = 지금 유효한 사실
```

로 분리했다.

그 다음에는 개별 문서보다 문서와 코드가 왜 존재하는지 알려주는 관계가 중요하다는 점을 발견했다. 이것이 Project Knowledge Graph로 발전했다.

## 2. 목적

프로젝트의 진실을 문서 더미가 아니라 다음 네 요소로 관리한다.

```text
Source of Truth
=
Current State
+
Relationships
+
Decision History
+
Evidence
```

## 3. 네 요소

### Current State

현재 실제로 적용되는 구조, 정책, 기술, 제약과 운영 상태

### Relationships

문제, 비전, 요구사항, 결정, 코드, 릴리스와 인시던트의 연결

### Decision History

왜 선택했는지 보존하는 ADR과 승인 이력

### Evidence

조사, 회의, 실험, 코드, 테스트, 사용자 피드백과 운영 데이터

## 4. 핵심 Node와 관계

```text
Problem
Vision
Requirement
Domain
Bounded Context
Decision
Service
API
Data
Task
Pull Request
Release
Incident
Evidence
```

```text
motivates
refines
constrains
decides
implements
depends_on
validates
replaces
affects
causes
learns_from
```

## 5. system_graph와 traceability

`system_graph`는 구조를 표현한다.

```text
주문 서비스 → depends_on → 결제 서비스
주문 API → uses → orders 테이블
```

`traceability`는 존재 이유와 이력을 표현한다.

```text
문제 P-1
→ 요구사항 REQ-3
→ 결정 ADR-2
→ PR #45
→ Release 1.2
```

## 6. 중앙 Graph 파일의 문제

한 개의 큰 `system_graph.yaml`이나 `traceability.yaml`을 여러 사람이 각자의 AI로 수정하면 Git 충돌과 중복이 발생한다.

현재 추천 방향은 분산 관계 선언이다.

```yaml
# ADR
id: ADR-2
decides:
  - REQ-3
```

```yaml
# PR metadata
refs:
  requirements:
    - REQ-3
  decisions:
    - ADR-2
  components:
    - payment-service
```

```yaml
# service metadata
id: payment-service
depends_on:
  - order-database
```

각 산출물이 자신이 직접 아는 관계를 기록하고, 스크립트가 이를 모아 `system_graph`와 `traceability` View를 생성한다.

```text
관계 원본 = 각 산출물
Graph = 자동 생성 파생 View
```

## 7. 검증 규칙

```text
Schema Validation
Reference Integrity
Duplicate Relation Check
Conflicting Relation Check
Replacement and Deletion Rules
Generated View Freshness
```

존재하지 않는 ID 참조, 오래된 관계와 Graph 갱신 누락은 CI에서 발견해야 한다.

## 8. Human View와 Agent View

```text
Human View = Markdown, 설명, 맥락, 다이어그램
Agent View = YAML, ID, 상태, 관계
```

두 View는 동일한 안정적 ID를 사용한다.

예:

```text
architecture.md
        ↕ ARCH-001
current_state.yaml
```

## 9. 결정 주체 기록

단순한 `approved: true`로는 AI가 결정한 것인지 사람이 선택한 것인지 알 수 없다.

```yaml
decision:
  id: ADR-017
  proposed_by: architecture_agent
  recommended_option: modular_monolith
  selected_option: modular_monolith
  selected_by_role: tech_lead
  recorded_by: documentation_agent
  evidence:
    - EVID-012
```

## 10. 개발자의 착각과 실패 패턴

- ADR을 많이 남기면 자동으로 지식 체계가 된다고 생각한다.
- Jira, GitHub, Wiki에 같은 사실을 편집해도 괜찮다고 생각한다.
- Knowledge Agent의 요약을 검증 없이 진실로 취급한다.
- 완벽한 Ontology를 먼저 만들려 한다.
- 중앙 Graph 파일 하나가 가장 단순하다고 생각한다.
- 자동 생성 View를 원본으로 편집한다.

## 11. 주요 파일

```text
current_state.yaml
domain_model.yaml
decision_index.yaml
relationship_schema.yaml
generated/system_graph.yaml 또는 동적 View
generated/traceability.yaml 또는 동적 View
```

## 12. 현재 합의와 미해결 사항

### 합의

- ADR은 Decision History다.
- Current State를 별도로 유지한다.
- 관계는 산출물 근처에서 분산 선언한다.
- Graph와 Traceability는 파생 View로 본다.
- 코드와 상태 Patch는 가능한 한 같은 PR에서 검토한다.

### 미해결

- 공통 관계 스키마
- 관계 삭제와 대체 방식
- Graph를 저장할지 동적으로 생성할지
- 코드와 상태 불일치 시 CI 실패 수준
- Graph DB 도입 임계점

## 13. 앞으로의 비전

02는 정적 문서 저장소에서 분산 메타데이터로 현재 상태와 관계 View를 만드는 Knowledge System으로 발전한다. 장기적으로 Agent는 전체 문서를 읽는 대신 Graph를 따라 필요한 근거만 조회하고, 사람은 쉬운 설명과 영향 범위를 통해 결정을 검토한다.

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
