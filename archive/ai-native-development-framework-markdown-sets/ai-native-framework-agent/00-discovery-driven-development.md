---
id: ANF-00
title: Discovery Driven Development
audience: ai-agent
status: draft
priority: highest
---
# 00. Discovery Driven Development

## 목적
고객과 확정 요구사항이 없는 1인 또는 3~5인 팀이 개발 전에 가치 있는 문제를 발견하고 검증한다.

## 시작 조건
- 막연한 아이디어, 불편, 관심 영역 중 하나가 존재한다.
- 솔루션과 기술 스택은 아직 확정하지 않는다.

## 처리 흐름
`idea -> observation -> problem -> evidence -> opportunity -> vision -> go/no-go`

## 필수 질문
1. 누가 어떤 상황에서 불편을 겪는가?
2. 현재 어떤 대안을 사용하며 왜 부족한가?
3. 문제의 빈도와 비용은 무엇인가?
4. 이 팀이 해결할 이유와 역량이 있는가?
5. 가장 작은 검증 방법은 무엇인가?

## 산출물
- `idea_space.yaml`
- `problem_space.yaml`
- `assumptions.yaml`
- `evidence.yaml`
- `vision.yaml`
- `decision.yaml`

## 에이전트 역할
- Discovery Agent: 관찰을 문제 후보로 변환한다.
- Research Agent: 외부 근거와 대안을 조사한다.
- Question Agent: 사용자가 만들지 못한 질문을 제안한다.
- Red-Team Agent: 해결책 편향과 확인 편향을 공격한다.

## 종료 기준
- 문제, 대상 사용자, 근거, 핵심 가정, 검증 방법이 기록되어 있다.
- `go`, `pivot`, `hold`, `stop` 중 하나가 승인되었다.

## 금지 사항
- 기술 선택으로 시작하지 않는다.
- 근거 없는 시장 규모와 사용자를 만들지 않는다.
- 질문을 한꺼번에 쏟지 않는다. 선택지와 예시를 사용한다.

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
