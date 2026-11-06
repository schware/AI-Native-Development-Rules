---
id: ANF-07
title: AI Native Context Architecture
audience: ai-agent
status: draft
---
# 07. AI Native Context Architecture

## 목적
최소한의 고신호 컨텍스트만 적시에 제공하여 토큰 비용과 오류를 줄인다.

## 컨텍스트 계층
1. Core: 목표, 제약, 역할, 현재 상태
2. Task: 작업 범위, 수용 기준, 관련 노드
3. Evidence: 필요한 ADR, 코드, 이슈의 선택된 부분
4. History: 요청이 있을 때만 조회하는 원문

## 로딩 정책
- 기본은 작은 `context_manifest.yaml`만 로드한다.
- 세부 자료는 ID와 관계를 이용해 Just-in-Time으로 조회한다.
- 재조회 가능한 대용량 결과는 장기 컨텍스트에 보존하지 않는다.
- 요약에는 원문 ID, 생성 시각, 신뢰 수준을 포함한다.

## 파일 구조
- `context_manifest.yaml`
- `current_state.yaml`
- `task_context.yaml`
- `retrieval_policy.yaml`
- `context_budget.yaml`

## 도구 계층
- GitHub: 코드, PR, 이력
- Jira: Epic, Story, Task
- Backstage 또는 카탈로그: 구성요소와 소유권
- 그래프 저장소: 관계와 영향도
- MCP/API: 컨텍스트와 도구의 표준화된 연결

## 토큰 최소화 원칙
- 문서 전체보다 식별자와 요약을 우선한다.
- 역할별로 다른 컨텍스트 뷰를 제공한다.
- 중복, 오래된 정보, 도구 출력은 제거한다.
- 비용 감소가 정확성이나 추적성을 훼손하지 않도록 평가한다.

## 접근성
사람용 Markdown과 Agent용 YAML을 함께 제공하고, 사람이 언제든 근거를 확인할 수 있게 한다.

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
