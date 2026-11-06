---
id: ANF-02
title: Project Knowledge Graph and Source of Truth
audience: ai-agent
status: draft
---
# 02. Project Knowledge Graph & Source of Truth

## 정의
Source of Truth는 `current state + relationships + decision history + evidence`다.

## 우선순위
1. 현재 상태
2. 승인된 요구사항과 정책
3. 관계 및 추적 정보
4. 근거와 ADR
5. 회의록과 원자료

## 핵심 노드
`problem, vision, requirement, domain, bounded_context, decision, service, api, data, task, pull_request, release, incident`

## 핵심 관계
`motivates, refines, constrains, decides, implements, depends_on, validates, replaces, releases, causes, learns_from`

## 저장 원칙
- ADR은 현재 상태가 아니라 결정 이력이다.
- 동일 사실을 여러 시스템에서 편집하지 않는다.
- 현재 상태는 작고 명시적이며 기계 검증 가능해야 한다.
- 모든 핵심 항목은 안정적인 ID와 출처를 가진다.

## 필수 파일
- `current_state.yaml`
- `domain_model.yaml`
- `system_graph.yaml`
- `traceability.yaml`
- `decision_index.yaml`

## 접근성
- Agent View: YAML과 그래프 질의
- Human View: Markdown 설명과 다이어그램
- 두 뷰는 동일한 ID를 공유하며 자동 검증한다.

## 실패 모드
- 문서 창고화, 진실의 중복, 끊어진 링크, 오래된 상태
- 근거 없는 자동 요약, 그래프 과잉 모델링, 의미가 다른 용어의 병합

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
