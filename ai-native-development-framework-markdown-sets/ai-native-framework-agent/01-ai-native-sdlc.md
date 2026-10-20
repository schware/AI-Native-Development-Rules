---
id: ANF-01
title: AI Native SDLC
audience: ai-agent
status: draft
---
# 01. AI Native SDLC

## 목적
검증된 문제를 배포하고 학습 가능한 시스템으로 전환한다.

## 생명주기
`vision -> specification -> domain -> architecture -> plan -> implement -> verify -> release -> operate -> learn`

## 단계별 계약
- 각 단계는 입력, 출력, 승인자, 검증 규칙, 추적 ID를 가진다.
- 다음 단계는 이전 단계의 승인된 산출물만 기준으로 삼는다.
- 불확실성은 숨기지 않고 `assumption`, `risk`, `unknown`으로 기록한다.

## 인간의 책임
- 목표와 우선순위 결정
- 되돌리기 어렵거나 고위험인 결정 승인
- 사용자 가치, 윤리, 보안, 출시 승인

## 에이전트의 책임
- 질문 생성, 문서화, 대안 분석, 구현, 테스트, 요약
- 근거와 변경 사항을 추적 가능한 형태로 제출
- 권한 밖의 결정은 중단하고 승격

## 개발자의 주요 착각
- 빠른 코드 생성이 빠른 제품 성공을 의미한다.
- 에이전트가 모호한 요구사항을 자동으로 올바르게 해석한다.
- 테스트 통과가 사용자 가치와 운영 안전을 증명한다.
- 에이전트를 늘리면 품질이 자동으로 오른다.

## 주요 실패 모드
- Context Drift, State Drift, Architecture Drift, Knowledge Drift
- 질문 피로, 과도한 자동화, 검토 병목, 책임 불명확

## 품질 게이트
- Discovery Gate, Design Gate, Implementation Gate, Release Gate, Learning Gate
- 각 게이트는 자동 검사와 인간 승인 조건을 분리한다.

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
