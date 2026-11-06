# 02. Project Knowledge Graph & Source of Truth

## 핵심 주장
프로젝트의 진실은 문서 한 개가 아니다. **현재 상태, 관계, 결정 이력, 근거**의 조합이다. 읽기 쉬운 문서만 축적하면 저장소는 창고가 되고, Agent가 모든 자료를 읽게 하면 비용과 오류가 증가한다.

## 네 계층
1. **현재 상태**: 지금 실제로 적용되는 구조, 정책, 기술, 제약
2. **관계**: 요구사항부터 코드, 릴리스, 인시던트까지의 연결
3. **결정 이력**: 왜 선택했는지 설명하는 ADR과 검토 이력
4. **근거**: 조사, 회의, 실험, 외부 자료와 원본 데이터

## Knowledge Graph 모델
노드는 문제, 비전, 요구사항, 도메인, 결정, 서비스, API, 데이터, 작업, PR, 릴리스, 인시던트를 포함한다. 관계는 `motivates`, `constrains`, `implements`, `depends_on`, `validates`, `replaces`, `learns_from`처럼 의미를 명확히 표현한다.

## ADR의 위치
ADR은 현재 상태를 매번 추론하기 위한 문서가 아니라 결정의 배경과 대안을 보존하는 추가 전용 이력이다. 현재 상태는 별도 파일에 명시하고, 해당 상태의 근거로 ADR ID를 연결한다.

## 이중 표현
- Human View: 설명, 맥락, 다이어그램을 담은 Markdown
- Agent View: 상태, ID, 관계를 담은 YAML 또는 그래프

두 형식은 동일 ID를 사용해야 하며, 자동 검사로 불일치를 찾아야 한다. YAML이 사람의 검토를 제거하는 수단이 되어서는 안 된다.

## 권장 핵심 파일
`current_state.yaml`, `domain_model.yaml`, `system_graph.yaml`, `traceability.yaml`, `decision_index.yaml`

## 접근성 문제
비개발자는 DDD와 그래프 용어를 모를 수 있다. Agent는 내부 모델을 자연어와 선택지로 번역해야 하며, 사용자가 결정의 의미, 영향 범위, 미확정 사항을 확인할 수 있어야 한다.

## 실패 패턴
문서 창고화, 여러 시스템의 중복 진실, 끊어진 연결, 오래된 상태, 근거 없는 요약, 과도한 온톨로지, 서로 다른 의미의 용어 병합이 대표적이다.

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
