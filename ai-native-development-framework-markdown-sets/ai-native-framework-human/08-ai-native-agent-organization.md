# 08. AI Native Agent Organization

## 정의
Agent Organization은 Agent 이름을 많이 만드는 작업이 아니다. 역할과 업무 경계를 정하고 각 역할의 입력, 출력, 권한, 검증, 중단 조건을 계약으로 만드는 일이다.

## 먼저 할 판단
정해진 절차라면 일반 코드나 Workflow를 우선한다. 불확실성과 판단이 필요한 부분에만 Agent를 쓴다. 단일 Agent로 충분하다면 Multi-Agent를 만들지 않는다.

## 역할 체계
- **Discovery Agent**: 문제 후보, 가설, 검증 계획
- **Question/Consultation Agent**: 사용자의 질문 부담을 낮추는 단계적 인터뷰
- **Documentation Agent**: 대화를 검토 가능한 문서로 변환
- **DDD Agent**: 공통 언어, 경계, 도메인 관계
- **Architecture Agent**: 기술 대안, 비기능 요구, ADR 초안
- **Planning Agent**: Epic, Story, Task, 수용 기준
- **Coding Agent**: 제한된 범위의 구현과 PR
- **QA Agent**: 독립적 테스트, 보안, 회귀 검증
- **Deployment Agent**: 승인된 릴리스 배포
- **Operations Agent**: 지표, 로그, 인시던트 분석
- **Knowledge Agent**: 현재 상태, 그래프, 색인 갱신
- **Orchestrator**: 라우팅, 예산, 승인, 중단 관리

## Agent 계약
각 역할은 `purpose`, `inputs`, `outputs`, `tools`, `permissions`, `context_budget`, `approval`, `stop_conditions`, `evaluation`을 가진다. 산출물은 자유 대화보다 구조화된 파일이나 이벤트로 전달한다.

## 사용자 접근성
사용자는 내부 Agent 조직을 이해할 필요가 없다. 단일 상담 창구가 질문을 작게 나누고, 내부 결과를 쉬운 언어로 설명하며, 중요한 결정에서만 승인을 요청한다. 전문 용어는 숨기는 것이 아니라 필요한 순간에 번역한다.

## 소규모 팀의 MVP
1인 또는 3~5인 팀은 `Discovery/Consultation`, `Builder`, `Reviewer`, `Knowledge` 네 역할로 시작할 수 있다. 역할은 논리적 구분이며 반드시 서로 다른 모델이나 프로세스일 필요는 없다.

## 분리 원칙
수행자와 검증자를 분리하고, 고위험 배포와 상태 갱신은 승인 후 병합한다. Knowledge Agent가 생성한 상태도 자동 진실로 취급하지 않고 코드와 테스트로 검증한다.

## 실패 패턴
역할 중복, 컨텍스트 복제, 무한 위임, 자기검증 편향, 권한 과다, 비용 폭증, Agent 간 가정 충돌이 대표적이다.

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
