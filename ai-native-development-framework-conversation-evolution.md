# AI Native Development Framework 대화 발전 기록

## 문서 목적

이 문서는 AI Agent를 활용한 개발 방향을 고민하면서, 처음의 단순한 질문이 어떻게 하나의 개발 프레임워크로 확장되었는지를 기록한다.

최종 결론만 제시하는 것이 아니라 다음 내용을 함께 보존한다.

- 어떤 문제의식에서 출발했는가
- 대화 중 어떤 착각과 한계를 발견했는가
- 왜 새로운 개념과 문서가 추가되었는가
- 각 문서가 어떤 책임을 가지게 되었는가
- 최종적으로 00, 01, 02, 07, 08이 어떻게 하나의 순환 구조를 이루는가

이 문서는 현재의 결론을 영구적인 정답으로 선언하지 않는다. 이후 AI Agent와 토론하고 실제 프로젝트에 적용하면서 수정하기 위한 프레임워크의 사고 이력이다.

---

# 1. 최초의 문제의식

대화는 AI Agent를 이용한 코딩의 방향성을 정리하려는 생각에서 시작되었다.

처음의 가정은 비교적 단순했다.

```text
문서를 정리한다
→ 하고 싶은 것을 찾는다
→ AI Agent에게 전달한다
→ AI Agent가 개발한다
```

이 단계에서 발견한 첫 번째 핵심은 코딩보다 먼저 해야 할 일이 있다는 점이었다.

> AI Agent를 이용한 개발의 시작점은 코드 생성이 아니라 프로젝트 문서와 의도를 정리하는 것이다.

AI가 코드를 빠르게 만들 수 있어도 다음이 불명확하면 프로젝트는 잘못된 방향으로 빠르게 진행된다.

- 무엇을 만들 것인가
- 왜 만드는가
- 누가 사용할 것인가
- 어떤 문제가 있는가
- 현재 시스템은 어떤 상태인가
- 어떤 제약을 지켜야 하는가

따라서 코딩 능력보다 문제 정의와 Context 정리가 더 중요한 병목이 될 수 있다는 가설이 만들어졌다.

---

# 2. GitHub와 Jira로 논의가 확장되다

문서를 정리한다는 생각은 자연스럽게 GitHub와 Jira의 관계로 확장되었다.

초기 구상은 다음과 같았다.

```text
문서
→ GitHub
→ Issue
→ Jira
→ AI Agent
→ Code
→ Pull Request
→ 문서 갱신
```

GitHub를 단순한 코드 저장소가 아니라 프로젝트 지식이 연결되는 공간으로 보려는 접근이었다.

Jira는 업무를 다음 단계로 분해하는 역할을 맡는다.

```text
Vision
→ Epic
→ Story
→ Task
→ Pull Request
→ Release
```

여기서 중요한 개념으로 Traceability가 등장했다.

```text
이 기능은 왜 존재하는가?
이 클래스는 어떤 요구사항을 구현하는가?
이 기술 선택은 어떤 결정에서 나왔는가?
이 변경은 어떤 릴리스에 포함되었는가?
```

이 질문에 답하려면 문서, 업무, 코드와 릴리스가 서로 연결되어야 한다.

---

# 3. ADR이 쌓이면 GitHub도 창고가 된다는 문제

다음으로 ADR을 축적하는 방식 자체에 문제가 제기되었다.

ADR을 잘 작성하더라도 수백 개가 쌓이면 다음 문제가 발생한다.

- 사람이 전부 읽기 어렵다
- Agent가 현재 유효한 결정을 찾기 위해 많은 토큰을 소비한다
- 서로 대체된 결정이 함께 남는다
- 현재 상태를 과거 결정 기록에서 매번 추론해야 한다
- 문서가 지식 체계가 아니라 기록 창고가 된다

처음에는 ADR에 상태를 추가하는 방식이 제안되었다.

```text
Proposed
Accepted
Superseded
Deprecated
Archived
```

하지만 곧 더 근본적인 문제가 발견되었다.

> 상태를 확인하기 위해서도 결국 ADR 문서를 읽어야 한다.

즉 ADR 상태 관리는 필요하지만, Agent의 Context 비용 문제를 근본적으로 해결하지는 못한다.

이 논의를 통해 ADR의 역할이 재정의되었다.

```text
ADR = 현재 상태가 아니라 결정 이력
```

현재 상태는 별도로 작고 명시적인 형태로 존재해야 한다.

```yaml
architecture:
  backend: spring-boot
  frontend: nextjs
  database: postgresql
  auth: oauth2
```

Agent는 먼저 현재 상태를 읽고, 결정의 이유가 필요할 때만 관련 ADR을 조회한다.

```text
Current State
→ 필요한 관계 확인
→ 필요한 ADR만 조회
```

이것이 이후 Source of Truth와 Context Architecture의 출발점이 되었다.

---

# 4. 문서에서 그래프로 관점이 이동하다

문서를 줄이는 것만으로는 충분하지 않았다. 문서와 코드가 왜 존재하는지 이해하려면 관계가 필요했다.

그래프는 특정 제품이나 그래프 데이터베이스만을 뜻하지 않는다.

```text
Node + Relationship
```

프로젝트에서 노드는 다음과 같은 객체다.

```text
Problem
Vision
Requirement
Epic
Story
ADR
Service
API
Database
Pull Request
Release
Incident
```

관계는 다음과 같은 의미를 가진다.

```text
motivates
refines
constrains
implements
depends_on
validates
replaces
affects
learns_from
```

예를 들어 다음 연결을 만들 수 있다.

```text
Problem
→ motivates
→ Vision
→ refined_by
→ Requirement
→ decided_by
→ ADR
→ implemented_by
→ Pull Request
→ included_in
→ Release
```

이 구조가 있으면 Agent는 모든 문서를 읽지 않고 필요한 관계를 따라갈 수 있다.

```text
질문
→ 관련 노드 조회
→ 연결된 현재 상태 확인
→ 필요한 근거 문서만 열람
```

이 시점에서 GitHub는 문서를 쌓는 창고가 아니라 Project Knowledge Graph의 일부로 해석되기 시작했다.

---

# 5. Source of Truth가 문서에서 상태로 바뀌다

논의를 통해 Source of Truth는 단일 문서나 특정 도구가 아니라 다음 네 요소의 결합으로 정의되었다.

```text
Source of Truth
=
Current State
+
Relationships
+
Decision History
+
Evidence
```

## 5.1 Current State

현재 실제로 적용되는 구조, 기술, 정책과 제약이다.

## 5.2 Relationships

문제, 요구사항, 결정, 코드, 릴리스와 운영 결과의 연결이다.

## 5.3 Decision History

왜 그런 선택을 했는지 보존하는 ADR, 검토와 승인 이력이다.

## 5.4 Evidence

회의, 조사, 실험, 사용자 피드백, 운영 데이터와 외부 근거다.

이 정의는 이후 02 문서의 중심이 되었다.

---

# 6. 코딩보다 구조 설계가 먼저라는 방향

다음 논의는 개발자의 역할에 대한 질문으로 이어졌다.

```text
AI가 코딩을 한다면 개발자는 언어와 코드를 얼마나 알아야 하는가?
```

대화에서 도출된 방향은 다음과 같다.

- 개발자는 문법 전문가일 필요가 줄어들 수 있다
- 그러나 코드를 읽고 검증할 능력은 여전히 필요하다
- 구현보다 서비스 경계, 데이터 흐름, 보안, 트랜잭션과 운영을 판단하는 능력이 중요해진다
- 코딩을 몰라도 된다는 뜻이 아니라 언어 중심 사고에서 구조 중심 사고로 이동한다는 뜻이다

개발자의 중심 업무는 다음으로 이동한다.

```text
문제 정의
도메인 구조화
설계와 의사결정
Context 구성
Agent 업무 분리
결과 검증
운영 학습
```

이 변화는 AI Native SDLC의 필요성을 만들었다.

---

# 7. 기존 SDLC에서 AI Native SDLC로

기존 개발 생명주기는 대체로 다음과 같다.

```text
Requirement
→ Design
→ Implementation
→ Test
→ Release
→ Operation
```

AI Native 환경에서는 그 이전과 이후가 확장된다.

```text
Intent
→ Consultation
→ Specification
→ Domain Modeling
→ Architecture
→ Planning
→ Implementation
→ Verification
→ Release
→ Operation
→ Knowledge Update
```

그러나 이 흐름도 아직 요구사항이나 Intent가 존재한다는 가정을 갖고 있었다.

뒤의 논의에서 고객과 요구사항이 없는 1인 또는 소규모 팀의 상황이 추가되면서 SDLC 앞에 별도의 Discovery 단계가 필요해졌다.

---

# 8. Workflow가 등장하면서 Multi-Agent와 역할 분리가 필요해지다

AI Native SDLC를 실제로 수행하려면 “어떤 단계가 있는가”만으로는 부족했다.

다음 질문이 생겼다.

```text
각 단계의 일을 누가 하는가?
하나의 Agent가 모든 일을 하는가?
업무별 Agent를 분리해야 하는가?
```

처음에는 하나의 Agent가 분석, 설계, 코딩, 테스트와 문서화를 모두 수행할 수도 있다고 보았다.

하지만 다음 위험이 발견되었다.

- Context가 지나치게 커진다
- 역할과 책임이 불명확해진다
- 자신이 작성한 결과를 자신이 검증하게 된다
- 각 단계의 가정이 섞인다
- 필요한 권한의 범위가 커진다

이에 따라 Agent Role Engineering 개념이 등장했다.

```text
Consultation Agent
Documentation Agent
DDD Agent
Architecture Agent
Planning Agent
Coding Agent
QA Agent
Deployment Agent
Operations Agent
Knowledge Agent
```

이 역할들은 곧바로 별도의 프로그램이나 모델을 뜻하지 않는다. 먼저 업무 책임을 논리적으로 분리하는 것이다.

이후 이 내용은 08 AI Native Agent Organization으로 독립했다.

---

# 9. Knowledge Agent가 핵심 역할로 부상하다

여러 Agent가 산출물을 만들면 다시 문서 창고 문제가 발생한다.

```text
Architecture Agent → ADR 생성
Coding Agent → PR 생성
QA Agent → 테스트 결과 생성
Deployment Agent → 릴리스 결과 생성
Operations Agent → 인시던트 기록 생성
```

누군가는 이 결과를 현재 상태와 관계에 반영해야 한다.

그래서 Knowledge Agent 역할이 중요해졌다.

Knowledge Agent의 목적은 문서를 더 많이 만드는 것이 아니다.

```text
Current State 갱신
Knowledge Graph 갱신
Traceability 갱신
Context 압축
오래된 상태 감지
충돌 후보 제안
```

그러나 Knowledge Agent의 결과를 곧바로 진실로 취급해서는 안 된다. 코드, 테스트, 승인된 결정과 대조한 뒤 병합해야 한다.

---

# 10. 토큰 비용이 Context Architecture를 만들다

Agent가 많아질수록 동일한 문서를 반복해서 읽는 비용이 증가한다.

이 문제는 단순한 비용 문제가 아니다.

- 많은 정보가 들어갈수록 중요한 정보가 흐려질 수 있다
- 오래된 정보가 현재 상태와 충돌할 수 있다
- 각 Agent가 서로 다른 문서 조합을 읽으면 가정이 달라질 수 있다
- 대용량 도구 결과가 작업 Context를 점유할 수 있다

이 문제에서 다음 원칙이 나왔다.

> 모든 문서를 읽히지 말고, 작업에 필요한 최소한의 고신호 Context를 적시에 제공한다.

Context는 다음 계층으로 구분한다.

```text
Core Context
Task Context
Evidence Context
Historical Context
```

Agent는 다음 순서로 정보를 읽는다.

```text
Context Manifest
→ Current State
→ Task Context
→ Related Graph Nodes
→ 필요한 Evidence
→ 필요할 때만 원문
```

이 개념이 07 AI Native Context Architecture로 발전했다.

---

# 11. Markdown과 YAML의 이중 구조

사람을 위해서는 설명과 배경이 필요하고, Agent를 위해서는 작고 구조화된 상태가 필요하다.

따라서 하나의 표현만으로는 부족하다.

## 사람용 표현

```text
Markdown
다이어그램
설명
대안과 트레이드오프
```

## Agent용 표현

```text
YAML
ID
관계
명시적 상태
권한과 계약
```

이 논의를 통해 Dual Documentation 원칙이 등장했다.

```text
Human View + Agent View
```

예:

```text
architecture.md
       ↕ ARCH-001
current_state.yaml
```

두 형식은 동일 ID로 연결되고 자동 검사로 불일치를 찾아야 한다.

YAML은 Markdown을 대체하는 것이 아니다. YAML은 Agent가 읽기 위한 압축된 상태이며, 사람은 Markdown을 통해 의미와 근거를 검토한다.

---

# 12. 사용자 접근성 문제가 추가되다

지금까지의 구조는 Agent와 시스템 중심이었다.

하지만 실제 사용자는 다음을 모를 수 있다.

- DDD
- ADR
- Knowledge Graph
- Bounded Context
- Context Budget
- Agent Orchestration

더 근본적인 문제는 사용자가 좋은 질문을 만들지 못할 수 있다는 점이었다.

기존 AI 활용은 다음을 암묵적으로 가정한다.

```text
좋은 질문
→ 좋은 답변
```

그러나 현실은 다음에 가깝다.

```text
막연한 생각
→ 무엇을 질문해야 할지 모름
→ 계속 질문을 요구받아 피로해짐
```

그래서 다음 역할이 추가되었다.

```text
Question Agent
Interview Agent
Explanation Agent
Teaching Agent
```

이 Agent들은 정답을 대신 결정하는 것이 아니라 사용자가 생각할 수 있도록 질문을 작게 나누고 선택지와 예시를 제공한다.

내부 Graph 표현도 사용자에게는 쉬운 언어로 번역해야 한다.

```yaml
order_service:
  depends_on:
    - payment_service
```

사용자에게는 다음처럼 설명한다.

```text
주문 기능은 결제 기능에 의존합니다.
결제 구조를 바꾸면 주문 취소와 완료 처리도 함께 확인해야 합니다.
```

사용자는 내부 Multi-Agent 구조를 알 필요 없이 하나의 상담 인터페이스와 대화할 수 있어야 한다.

---

# 13. 고객이 없는 1인 또는 3~5인 팀이라는 가정

프레임워크는 대기업 TF나 고객 프로젝트만을 위한 것이 아니었다.

오히려 다음 상황이 핵심 가정으로 추가되었다.

```text
고객 없음
확정 요구사항 없음
1인 또는 3~5인 팀
AI Agent와 함께 아이템 탐색
```

이 상황에서는 Requirement가 시작점이 될 수 없다.

실제 흐름은 다음과 같다.

```text
Curiosity
→ Idea Discovery
→ Problem Discovery
→ Question Generation
→ Evidence
→ Vision
→ Requirement
```

이에 따라 기존 01보다 앞에 00 Discovery Driven Development가 추가되었다.

---

# 14. 00 Discovery Driven Development의 탄생

00은 무엇을 만들지 정하는 기능 목록 문서가 아니다.

핵심 질문은 다음과 같다.

```text
어떤 문제가 존재하는가?
누가 그 문제를 겪는가?
현재 어떻게 해결하고 있는가?
그 대안은 왜 부족한가?
이 팀이 해결할 이유와 능력이 있는가?
가장 작은 검증은 무엇인가?
```

00의 흐름은 다음과 같다.

```text
Idea
→ Observation
→ Problem
→ Evidence
→ Assumption
→ Opportunity
→ Vision
→ Go / Pivot / Hold / Stop
```

이 단계에서 중요한 Agent는 Coding Agent가 아니다.

```text
Discovery Agent
Research Agent
Question Agent
Red-Team Agent
```

00의 결과물은 코드가 아니라 검증 가능한 문제 정의다.

```yaml
idea_space.yaml
problem_space.yaml
assumptions.yaml
evidence.yaml
opportunity.yaml
vision.yaml
decision.yaml
```

---

# 15. 개발자의 착각과 실패 패턴을 문서에 포함하다

방법론은 이상적인 흐름만 설명해서는 부족하다.

어디서 실패하는지도 함께 정의해야 한다.

## 대표적인 개발자의 착각

- AI가 코딩을 잘하니 설계가 덜 중요하다
- 문서를 많이 제공하면 AI가 더 잘 이해한다
- ADR을 많이 남기면 지식 관리가 된다
- Agent가 요구사항의 빈칸을 올바르게 채운다
- 테스트 통과가 사용자 가치와 운영 안전을 증명한다
- Multi-Agent가 단일 Agent보다 항상 좋다
- Knowledge Agent가 생성한 상태는 자동으로 진실이다
- 토큰을 줄이면 무조건 좋은 Context Architecture다

## 대표적인 실패 패턴

```text
Problem Drift
Context Drift
State Drift
Architecture Drift
Knowledge Drift
Scope Drift
질문 피로
승인 병목
역할 중복
무한 위임
과도한 권한
근거 없는 요약
문서 창고화
진실의 중복
```

이 내용은 특히 00, 01, 02, 07, 08 각각의 실패 조건으로 분산되어야 한다.

---

# 16. 최종 문서 체계

대화를 통해 최종적으로 다음 다섯 문서가 핵심 구조로 정리되었다.

## 00. Discovery Driven Development

```text
무엇을 왜 만들 것인가?
```

고객과 요구사항이 없는 상태에서 문제를 발견하고 검증한다.

## 01. AI Native SDLC

```text
발견한 문제를 어떻게 설계, 개발, 검증, 배포하고 학습할 것인가?
```

개발 생명주기와 인간 승인 지점을 정의한다.

## 02. Project Knowledge Graph & Source of Truth

```text
프로젝트의 진실을 어떤 상태와 관계로 표현할 것인가?
```

Current State, Relationships, Decision History와 Evidence를 정의한다.

## 07. AI Native Context Architecture

```text
각 Agent에게 무엇을 얼마나 읽힐 것인가?
```

토큰, 정확성, 보안과 추적성을 고려한 Context 공급 구조를 정의한다.

## 08. AI Native Agent Organization

```text
누가 어떤 책임과 권한으로 일할 것인가?
```

Agent 역할, 계약, 협업, 검증과 중단 조건을 정의한다.

---

# 17. 다섯 문서의 관계

```text
00은 문제를 발견하고 검증한다.

01은 검증된 문제를 개발 생명주기로 전환한다.

02는 생명주기에서 생성된 상태, 관계, 결정과 근거를 관리한다.

07은 02의 지식 중 각 작업에 필요한 부분만 Agent에게 제공한다.

08은 07의 Context를 이용하여 일하는 Agent 조직과 책임을 정의한다.
```

더 짧게 표현하면 다음과 같다.

```text
00 = 무엇을 왜 만들 것인가
01 = 어떻게 만들고 운영할 것인가
02 = 프로젝트의 진실은 무엇인가
07 = 무엇을 얼마나 읽힐 것인가
08 = 누가 어떤 책임으로 일할 것인가
```

---

# 18. 최종 순환 구조

```text
사람의 경험과 관찰
        ↓
00 문제 발견과 검증
        ↓
01 요구사항, 도메인, 설계, 구현과 운영
        ↓
02 상태, 관계, 결정 이력과 근거 축적
        ↓
07 작업별 최소 Context 구성
        ↓
08 Agent 역할별 수행과 독립 검증
        ↓
코드, 테스트, 배포와 운영
        ↓
Knowledge Agent의 상태 갱신 제안
        ↓
사람과 자동 검증을 거쳐 병합
        ↓
운영 데이터와 새로운 관찰
        ↓
다시 00
```

프레임워크의 목적은 한 번의 개발 완료가 아니라 학습 가능한 순환을 만드는 것이다.

---

# 19. 소규모 팀의 최소 구현

전체 프레임워크를 처음부터 모두 구축하면 오히려 과도한 설계가 될 수 있다.

1인 또는 3~5인 팀은 다음으로 시작할 수 있다.

## 최소 문서

```text
problem-space.md
vision.md
current-state.md
architecture.md
```

## 최소 Agent용 상태

```yaml
problem_space.yaml
vision.yaml
current_state.yaml
task_context.yaml
agent_roles.yaml
```

## 최소 역할

```text
Discovery / Consultation
Builder
Reviewer
Knowledge
```

## 최소 도구

```text
GitHub
Markdown
YAML
AI Agent 한 개 또는 소수의 역할별 세션
```

Jira, Backstage, 그래프 데이터베이스와 MCP는 실제로 검색, 관계, 권한 또는 통합 문제가 발생할 때 추가한다.

---

# 20. 향후 검증해야 할 핵심 가설

이 프레임워크는 다음 가설을 실제 프로젝트에서 검증해야 한다.

1. Current State 우선 접근이 문서 전체 검색보다 일관된 결과를 만드는가
2. Markdown과 YAML 이중 표현의 유지 비용이 얻는 가치보다 작거나 같은가
3. 역할별 Context 분리가 품질과 비용을 개선하는가
4. Knowledge Agent가 상태 불일치를 실제로 줄이는가
5. Question Agent가 사용자의 질문 피로를 줄이는가
6. Discovery 단계가 불필요한 구현을 줄이는가
7. 소규모 팀에서 네 역할 MVP가 충분한가
8. Multi-Agent 전환이 필요한 명확한 임계 조건을 정의할 수 있는가
9. 토큰 최소화가 중요한 예외와 맥락을 손실하지 않는가
10. 운영 결과가 00의 새로운 Discovery로 실제 환류되는가

---

# 21. 최종 정의

> AI Native Development Framework는 사람이 완성된 질문과 요구사항을 AI에게 명령하는 방식이 아니다. 사람이 경험, 의도와 판단을 제공하면 AI가 필요한 질문을 함께 만들고, 그 결과를 상태와 관계로 구조화하며, 명시적인 역할과 권한을 가진 Agent들이 이를 구현하고 독립적으로 검증하고 운영하면서 프로젝트의 지식을 지속적으로 갱신하는 개발 방식이다.

이 프레임워크에서 코드는 중요한 산출물이지만 유일한 자산은 아니다.

진짜 장기 자산은 다음의 연결이다.

```text
Problem
Vision
Requirement
Domain
Decision
Current State
Context
Agent Contract
Code
Release
Operation
Learning
```

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
