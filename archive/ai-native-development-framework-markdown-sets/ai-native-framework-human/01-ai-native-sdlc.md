# 01. AI Native SDLC

## 정의
AI Native SDLC는 AI가 코드를 대신 쓰는 절차가 아니다. 사람이 목표와 승인 책임을 맡고, 에이전트가 질문, 분석, 구현, 검증을 지원하며, 모든 결과를 다음 작업에 재사용 가능한 지식으로 환류하는 개발 생명주기다.

## 전체 흐름
`Vision → Specification → Domain Modeling → Architecture → Planning → Implementation → Verification → Release → Operation → Learning`

## 단계 설계
각 단계에는 입력, 출력, 책임자, 승인 조건, 검증 규칙과 추적 ID가 있어야 한다. 모호한 대화를 다음 단계로 넘기지 않고, 검토 가능한 산출물로 바꾼 뒤 이동한다.

### 1. Vision과 Specification
00의 검증된 문제를 사용자 목표, 범위, 비범위, 제약, 성공 기준으로 변환한다. AI는 누락 질문을 만들지만 답을 임의로 확정하지 않는다.

### 2. Domain과 Architecture
DDD를 이용해 공통 언어와 경계를 만들고, 기술 선택은 기능 요구뿐 아니라 보안, 비용, 운영, 팀 역량, 되돌리기 가능성을 함께 고려한다. 중요한 선택은 ADR로 남긴다.

### 3. Planning과 Implementation
작업은 작은 수용 기준으로 분해한다. 코딩 에이전트는 승인된 범위에서만 수정하고, 변경 이유와 테스트 결과를 PR에 남긴다.

### 4. Verification과 Release
테스트 통과와 제품 성공을 구분한다. 기능, 회귀, 보안, 성능, 접근성, 운영 가능성을 확인하고 고위험 변경은 인간이 승인한다.

### 5. Operation과 Learning
로그, 지표, 사용자 피드백, 인시던트를 새로운 발견 입력으로 되돌린다. 운영은 생명주기의 끝이 아니라 00으로 돌아가는 학습 단계다.

## 사람과 Agent의 경계
사람은 가치, 우선순위, 위험 수용, 출시를 결정한다. Agent는 대안과 근거를 만들고 반복 작업을 수행한다. 불확실하거나 권한 밖인 경우 Agent는 중단하고 사람에게 승격해야 한다.

## 개발자의 착각
- AI의 코딩 속도를 전체 프로젝트 속도로 착각한다.
- 질문하지 않은 요구사항도 AI가 알아서 올바르게 채울 것으로 본다.
- 테스트 통과를 아키텍처 적합성과 사용자 가치의 증명으로 본다.
- 에이전트 수가 많으면 전문성과 품질이 자동으로 오른다고 생각한다.

## 주요 이슈
Context Drift, State Drift, Architecture Drift, Knowledge Drift, 질문 피로, 승인 병목, 과도한 자동화, 책임 불명확이 핵심 위험이다.

## 품질 게이트
Discovery, Design, Implementation, Release, Learning 게이트를 두고 자동 검사와 사람 승인을 분리한다. 작은 팀에서는 게이트 수를 줄이되 되돌리기 어려운 결정과 운영 위험은 생략하지 않는다.

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
