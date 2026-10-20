# 07. AI Native Context Architecture

## 목적
어떤 문서를 저장할지보다, 각 에이전트에게 어떤 정보를 언제 얼마나 제공할지 설계한다. 토큰 절약은 목표가 아니라 정확성, 비용, 추적성을 함께 최적화하는 제약이다.

## 계층형 Context
- **Core Context**: 목표, 역할, 권한, 제약, 현재 상태
- **Task Context**: 이번 작업의 범위, 수용 기준, 관련 노드
- **Evidence Context**: 필요한 ADR, 코드, 이슈의 선택된 부분
- **Historical Context**: 필요할 때만 조회하는 원문

에이전트는 처음부터 전체 저장소를 읽지 않는다. 작은 `context_manifest.yaml`에서 시작해 ID와 관계로 필요한 자료를 Just-in-Time 조회한다.

## Human View와 Agent View
Markdown은 설명과 토론을 위한 형식이고 YAML은 상태와 계약을 압축하기 위한 형식이다. 둘 중 하나만 사용하면 각각 토큰 낭비 또는 인간 검토 상실 문제가 생긴다. 두 뷰를 같은 ID로 연결하고 자동 검증한다.

## 권장 파일
- `context_manifest.yaml`: 기본 로딩 항목
- `current_state.yaml`: 현재 사실과 정책
- `task_context.yaml`: 작업별 최소 컨텍스트
- `retrieval_policy.yaml`: 조회 순서와 허용 소스
- `context_budget.yaml`: 역할별 예산과 축약 정책

## Tooling Architecture
GitHub는 코드와 변경 이력, Jira는 작업 관계, Backstage 또는 유사 카탈로그는 구성요소와 소유권, 그래프 저장소는 관계와 영향도, MCP/API는 Agent와 외부 시스템의 연결을 담당한다. 도구를 Source of Truth로 선언하기 전에 어떤 데이터의 권위 소스인지 먼저 정한다.

## 최소화 전략
중복 제거, 고신호 요약, 역할별 뷰, 지연 로딩, 오래된 도구 결과 삭제, 안정적 식별자를 적용한다. 요약에는 원문 링크, 생성 시점, 생성 주체, 신뢰 수준을 넣는다.

## 위험
Context Rot, 중요한 예외의 압축 손실, 오래된 캐시, 권한이 다른 정보의 혼합, MCP 도구 과다, YAML 스키마의 조기 고정이 있다.

## 단계적 도입
처음에는 GitHub와 소수 YAML 파일로 시작한다. 검색과 추적 문제가 실제로 발생할 때 Jira, 카탈로그, 그래프 저장소, MCP를 단계적으로 추가한다.

## 참고 문서

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
