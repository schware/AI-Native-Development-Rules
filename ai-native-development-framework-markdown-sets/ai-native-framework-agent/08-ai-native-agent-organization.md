---
id: ANF-08
title: AI Native Agent Organization
audience: ai-agent
status: draft
---
# 08. AI Native Agent Organization

## 목적
에이전트의 역할, 권한, 입출력, 협업, 중단 조건을 명시한다.

## 기본 원칙
- 먼저 단일 에이전트 또는 결정적 워크플로를 검토한다.
- 역할 분리가 품질, 보안, 컨텍스트 격리에 실익이 있을 때만 다중 에이전트를 사용한다.
- 모든 에이전트는 최소 권한과 명시적 산출물 계약을 가진다.

## 역할
- Discovery: 문제 후보와 가설 생성
- Question/Consultation: 단계적 질문과 선택지 제공
- Documentation: 대화를 승인 가능한 문서로 변환
- DDD: 용어, 경계, 도메인 관계 정의
- Architecture: 기술 대안, ADR, 비기능 요구 분석
- Planning: Epic, Story, Task와 수용 기준 생성
- Coding: 제한된 범위의 코드와 PR 생성
- QA: 독립적 테스트, 보안 및 회귀 검증
- Deployment: 승인된 릴리스의 배포 실행
- Operations: 지표, 로그, 인시던트 분석
- Knowledge: 현재 상태, 그래프, 색인 갱신
- Orchestrator: 라우팅, 예산, 승인, 중단 관리

## 역할 계약 필드
`id, purpose, inputs, outputs, tools, permissions, context_budget, approval, stop_conditions, evaluation`

## 협업 규칙
- 자유로운 에이전트 간 대화 대신 구조화된 산출물을 전달한다.
- 수행자와 검증자는 가능한 한 분리한다.
- 충돌 시 Source of Truth와 인간 승인 규칙을 따른다.
- Knowledge Agent의 갱신은 검증 후 병합한다.

## 소규모 팀 MVP
`Discovery/Consultation + Builder + Reviewer + Knowledge`

## 주요 위험
역할 중복, 컨텍스트 복제, 무한 위임, 자기검증 편향, 권한 과다, 비용 폭증.

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
