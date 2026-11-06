# 00. Discovery Driven Development

## 이 문서가 필요한 이유
고객이 요구사항을 건네는 프로젝트가 아니라 혼자 또는 3~5명이 시작하는 프로젝트에서는, 코딩보다 먼저 “무엇을 왜 만들 것인가”를 찾아야 한다. AI는 모호한 아이디어를 빠르게 구현할 수 있지만, 잘못 고른 문제도 빠르게 제품으로 만들어 버린다.

## 목표
막연한 관심과 불편을 검증 가능한 문제 정의로 바꾸고, 개발 여부를 결정한다. 이 단계에서는 기술 스택과 기능 목록을 서둘러 확정하지 않는다.

## 권장 흐름
1. **관찰 수집**: 반복해서 불편한 일, 수작업, 대기, 오류, 정보 단절을 기록한다.
2. **문제 후보화**: 해결책 표현을 제거하고 누가 어떤 상황에서 무엇 때문에 어려운지 쓴다.
3. **외부 조사**: 기존 대안, 유사 서비스, 공개 사례, 규제와 기술 제약을 조사한다.
4. **가정 분리**: 사실, 해석, 가정, 희망을 구분한다.
5. **질문 생성**: 사용자가 떠올리지 못한 질문을 AI가 제안하되, 한 번에 적은 수의 질문과 선택지를 제공한다.
6. **작은 검증**: 인터뷰, 수동 서비스, 프로토타입, 데이터 확인 등 가장 싼 검증을 선택한다.
7. **결정**: 진행, 전환, 보류, 중단을 기록한다.

## AI Agent의 역할
Discovery Agent는 문제 후보를 만들고, Research Agent는 외부 근거를 수집한다. Question Agent는 사용자의 질문 부담을 낮추며, Red-Team Agent는 편향과 과장된 가정을 공격한다. 최종 선택은 사람이 한다.

## 산출물
`idea_space.yaml`, `problem_space.yaml`, `assumptions.yaml`, `evidence.yaml`, `vision.yaml`, `decision.yaml`을 권장한다. Markdown은 사람이 읽는 설명이고 YAML은 다음 에이전트가 읽을 압축된 상태다.

## 실패하기 쉬운 지점
- 흥미로운 기술을 문제로 착각한다.
- 사용자나 시장을 확인하지 않고 기능을 확장한다.
- AI가 제안한 수치와 사례를 근거 없이 사실로 취급한다.
- 질문이 많아져 사용자가 결정을 포기한다.

## 완료 기준
대상 사용자, 문제 상황, 기존 대안, 핵심 근거, 가장 위험한 가정, 다음 검증 방법이 명확하고 진행 여부가 승인되어야 한다.

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
