# AI Native Development Framework v0.3

## 이 패키지의 목적

이 패키지는 AI Agent를 이용한 코딩 도구 비교에서 시작한 대화가 어떻게 문제 발견, 개발 생명주기, 프로젝트 지식, Context Architecture와 Agent Organization으로 발전했는지를 보존한다.

이전 문서 세트의 문제는 최종 흐름과 산출물은 있었지만, 왜 그런 구조에 도달했는지에 대한 대화 압축과 판단 근거가 부족했다는 점이다. 이번 버전은 각 문서 안에 다음 네 층을 함께 넣는다.

```text
대화에서 발견한 문제
→ 방향을 바꾼 판단 근거
→ 현재 명세와 합의
→ 앞으로의 비전과 실험 과제
```

## 권장 읽기 순서

1. `00-discovery-driven-development.md`
2. `01-ai-native-sdlc.md`
3. `02-project-knowledge-graph-source-of-truth.md`
4. `07-ai-native-context-architecture.md`
5. `08-ai-native-agent-organization.md`

## 전체 관계

```text
00 = 무엇을 왜 만들 것인가
01 = 어떻게 만들고 운영하며 학습할 것인가
02 = 프로젝트의 진실과 관계는 무엇인가
07 = 어떤 Context를 누구에게 얼마나 제공할 것인가
08 = 누가 어떤 책임과 권한으로 일할 것인가
```

```text
사람의 경험과 관찰
→ 00 문제 발견과 선택
→ 01 설계, 구현, 검증, 운영과 학습
→ 02 상태, 관계, 결정 이력과 근거 축적
→ 07 작업별 최소 Context 구성
→ 08 역할별 Agent 수행과 독립 검증
→ 코드, 릴리스와 운영 결과
→ Knowledge 갱신
→ 다시 00
```

## 현재 적용 범위

우선 대상은 고객과 확정 요구사항이 없는 1인 또는 3~5인 팀이다. 대기업 TF나 다수 조직으로 확장할 수 있지만, 처음부터 복잡한 도구와 Multi-Agent 시스템을 구축하지 않는다.

## 공통 원칙

- AI는 선택지, 근거와 추천을 제시한다.
- Decision Owner 역할을 맡은 사람이 실제 결정을 내린다.
- AI는 사람의 결정을 기록한다.
- 모든 산출물을 같은 깊이로 검토하지 않는다.
- Current State는 작고 명시적으로 유지한다.
- ADR은 현재 상태가 아니라 결정 이력이다.
- 관계는 산출물 근처에서 분산 선언하고 Graph View는 자동 생성하는 방향을 우선 검토한다.
- 특정 제품 사용법은 본문이 아니라 부록으로 분리한다.

---

# 참고 문서

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
