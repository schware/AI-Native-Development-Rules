# AI Native Development Framework

## 대화 발전 과정, 현재 구조, 협의 사항과 앞으로의 비전

**문서 상태:** Working Draft v0.2  
**대상:** 사람과 AI Agent가 함께 읽는 공통 Context 문서  
**적용 범위:** 고객이 명확하지 않은 1인 개발 또는 3~5인 소규모 팀을 우선 대상으로 하되, 이후 팀과 조직 단위로 확장 가능

---

# 1. 이 문서를 다시 작성한 이유

이 프레임워크의 첫 번째 문서 세트는 00, 01, 02, 07, 08의 최종 흐름과 산출물 위주로 작성되었다. 그 결과 문서만 읽은 사람이나 다른 AI Agent는 다음 내용을 알기 어려웠다.

- 왜 문서화가 코딩보다 먼저라고 판단했는가
- 왜 ADR을 쌓는 것만으로는 부족하다고 보았는가
- 왜 `current_state`가 별도로 필요해졌는가
- 왜 문서 목록에서 Knowledge Graph로 관점이 바뀌었는가
- 왜 YAML을 도입하려 했는가
- 왜 Coding Agent보다 Discovery Agent와 Knowledge Agent를 중요하게 보았는가
- 왜 사용자에게 계속 질문하도록 요구하는 방식이 한계라고 판단했는가
- 어떤 사항이 합의되었고 어떤 사항이 아직 제안 또는 검증 대상인가

즉, 이전 문서는 **어디에 도착했는가**는 보여주었지만 **왜 그곳에 도착했는가**는 충분히 보여주지 못했다.

이번 문서는 다음 네 층을 함께 보존한다.

```text
대화 발전 과정
→ 판단 근거와 문제 제기
→ 현재 프레임워크 명세
→ 앞으로의 실험과 비전
```

이 문서는 단순한 소개서가 아니다. 이후 다른 AI Agent와 대화를 이어가기 위한 공통 기억이며, 이미 논의한 문제를 매번 처음부터 다시 검토하지 않도록 만드는 Context 문서다.

---

# 2. 최초의 출발점

처음의 관심은 “AI Agent를 이용해 어떻게 코딩할 것인가”였다. 그러나 대화를 진행하면서 실제 병목은 코딩이 아니라 그 이전에 있다는 점을 발견했다.

```text
무엇을 만들 것인가
왜 만들 것인가
무엇을 알고 있는가
무엇이 아직 불확실한가
AI에게 어떤 정보를 전달할 것인가
```

AI가 코드를 빠르게 생성해도 문제와 구조가 불명확하면 잘못된 방향으로 더 빠르게 진행할 뿐이다.

따라서 첫 번째 전환은 다음과 같았다.

```text
코딩 우선
→ 문서화 우선
→ 구조화 우선
→ Context 우선
```

이때 문서화는 개발 이후의 기록 작업이 아니라 개발 전 사고 과정이 되었다.

```text
작업하다가 생각나는 것을 추가
```

하는 방식보다,

```text
문서화하면서 질문과 구조를 추가
→ 틀이 어느 정도 만족스러워졌을 때 개발
```

하는 방식이 AI Agent 시대에 더 적합하다는 방향이 만들어졌다.

---

# 3. GitHub와 Jira에 대한 초기 구상

다음 고민은 정리된 문서를 GitHub와 Jira로 어떻게 발전시킬 것인가였다.

초기 흐름은 다음과 같았다.

```text
문서
→ GitHub
→ Issue
→ Jira의 Epic, Story, Task
→ AI Agent
→ Code와 Pull Request
→ 문서 갱신
```

이때 GitHub는 코드 저장소를 넘어 다음을 보존하는 장소로 보았다.

- 코드와 테스트
- 문서
- ADR
- 변경 이력
- Pull Request
- 릴리스 근거

Jira는 해야 할 일을 구조화하는 역할을 맡는다.

```text
Vision
→ Epic
→ Story
→ Task
→ PR
→ Release
```

이 논의를 통해 중요한 개념이 등장했다.

> 코드와 작업은 그것이 생겨난 문제와 결정까지 역추적할 수 있어야 한다.

이것이 Traceability의 출발점이었다.

---

# 4. ADR이 쌓이면 GitHub도 창고가 된다는 문제

처음에는 ADR에 상태를 넣고 다음과 같이 관리하는 방식을 생각했다.

```text
Proposed
Accepted
Superseded
Deprecated
Archived
```

그러나 중요한 반론이 나왔다.

> ADR의 상태를 확인하려면 결국 ADR을 읽어야 하고, 그것도 토큰 비용에 들어간다.

ADR이 수백 개 쌓이면 다음 문제가 생긴다.

- 현재 유효한 결정을 찾기 어렵다
- 대체된 결정과 현재 결정이 함께 검색된다
- 현재 구조를 과거 기록에서 매번 추론해야 한다
- 사람과 AI 모두 많은 문서를 읽어야 한다
- GitHub가 살아 있는 지식 체계가 아니라 축적 창고가 된다

여기서 ADR의 역할을 재정의했다.

```text
ADR = 현재 상태가 아니라 결정 이력
```

현재 상태는 별도로 작고 명시적인 형태로 관리해야 한다.

```yaml
architecture:
  backend: spring-boot
  frontend: nextjs
  database: postgresql
  auth: oauth2
```

Agent는 먼저 현재 상태를 읽고, 이유가 필요할 때 관련 ADR만 찾아야 한다.

```text
Current State
→ 관련 관계 확인
→ 필요한 ADR만 조회
```

이 전환이 02와 07의 핵심 토대가 되었다.

---

# 5. 문서 중심에서 그래프 중심으로

문서를 적게 읽게 하는 것만으로는 부족했다. 어떤 코드와 결정이 왜 존재하는지 알려면 문서 사이의 관계가 필요했다.

그래프는 특정 데이터베이스 제품을 뜻하는 것이 아니라 다음 구조를 뜻한다.

```text
Node + Relationship
```

예를 들어 다음은 모두 Node가 될 수 있다.

```text
Problem
Vision
Requirement
Domain
ADR
Epic
Task
Service
API
Table
Pull Request
Release
Incident
```

관계는 다음과 같이 표현할 수 있다.

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

예:

```text
문제 P-1
→ motivates
→ 비전 V-1
→ refined_by
→ 요구사항 REQ-3
→ decided_by
→ ADR-2
→ implemented_by
→ PR #45
→ included_in
→ Release 1.2
```

이 구조가 있다면 Agent는 모든 문서를 읽지 않고 관련 Node와 Edge를 따라 필요한 정보만 가져올 수 있다.

여기서 GitHub는 전체 Knowledge Graph 그 자체가 아니라 코드, PR, 이력과 근거를 제공하는 한 부분이 되었다.

---

# 6. Source of Truth의 재정의

대화를 통해 Source of Truth는 특정 문서나 특정 도구 하나가 아니라 다음 요소의 결합으로 정의되었다.

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

## 6.1 Current State

현재 실제로 적용되는 구조, 기술, 정책, 제약과 운영 상태다.

## 6.2 Relationships

문제, 비전, 요구사항, 결정, 코드, 릴리스와 운영 결과의 연결이다.

## 6.3 Decision History

ADR처럼 왜 그런 선택을 했는지 보존하는 이력이다.

## 6.4 Evidence

회의, 조사, 실험, 사용자 피드백, 코드, 테스트와 운영 데이터다.

이 정의를 통해 “문서를 많이 남기는 것”과 “지식을 유지하는 것”이 서로 다르다는 점이 명확해졌다.

---

# 7. 개발자 역할에 대한 관점 변화

AI가 코드를 생성하면 개발자가 언어나 코드를 몰라도 되는지 질문이 생겼다.

도출된 결론은 다음과 같다.

- 문법을 직접 작성하는 비중은 줄어들 수 있다
- 그러나 코드를 읽고 평가하는 능력은 필요하다
- 구현보다 서비스 경계, 데이터 흐름, 보안, 트랜잭션, 비용과 운영을 판단하는 능력이 중요해진다
- 개발자는 언어를 버리는 것이 아니라 언어 중심 사고에서 구조 중심 사고로 이동해야 한다

개발자의 중심 책임은 다음으로 이동한다.

```text
문제 정의
도메인 구조화
의사결정
아키텍처 설계
Context 설계
업무와 Agent 역할 분리
결과 검증
운영 학습
```

이 논의가 01 AI Native SDLC를 만들었다.

---

# 8. Workflow에서 Multi-Agent Organization으로

개발 생명주기를 정의하자 다음 질문이 생겼다.

```text
각 단계는 누가 수행하는가?
하나의 Agent가 전부 수행하는가?
업무별 역할을 분리해야 하는가?
```

하나의 Agent가 분석, 설계, 코딩, 테스트와 기록을 모두 맡으면 다음 문제가 생길 수 있다.

- Context가 커진다
- 책임이 섞인다
- 자신이 만든 것을 자신이 검증한다
- 단계별 가정이 섞인다
- 과도한 권한을 요구한다

이에 따라 다음 역할이 논의되었다.

```text
Discovery Agent
Question / Consultation Agent
Documentation Agent
DDD Agent
Architecture Agent
Planning Agent
Coding Agent
QA Agent
Deployment Agent
Operations Agent
Knowledge Agent
Orchestrator
```

중요한 점은 역할 수만큼 별도 모델이나 프로그램을 만드는 것이 아니다. 먼저 책임과 Context를 논리적으로 분리하는 것이다.

이 내용이 08 AI Native Agent Organization으로 발전했다.

---

# 9. Coding Agent보다 중요해진 Agent

논의를 진행하면서 Coding Agent만으로 프로젝트 전체를 운영할 수 없다는 점이 명확해졌다.

특히 세 역할이 중요하게 부상했다.

## 9.1 Discovery Agent

무엇을 만들어야 하는지 아직 모를 때 문제 후보와 가설을 만든다.

## 9.2 Question Agent

사용자가 만들지 못한 질문을 대신 제안하고, 질문 피로를 낮추기 위해 선택지와 예시를 제공한다.

## 9.3 Knowledge Agent

Agent들이 생성한 결과를 현재 상태와 관계에 반영하는 변경안을 만든다.

```text
ADR
PR
테스트 결과
릴리스 결과
인시던트
→ Current State와 Graph 갱신 후보
```

Knowledge Agent의 제안은 자동으로 진실이 되는 것이 아니라 코드, 테스트와 승인된 결정에 대해 검증한 뒤 병합해야 한다.

---

# 10. 사용자가 질문을 만들지 못하는 문제

AI 활용은 흔히 다음을 전제한다.

```text
좋은 질문
→ 좋은 답변
```

하지만 실제 사용자는 자신이 원하는 것을 정확히 설명하지 못할 수 있고, 어떤 질문을 해야 하는지조차 모를 수 있다.

```text
막연한 생각
→ 질문을 만들기 어려움
→ AI의 반복 질문
→ 질문 피로와 결정 포기
```

따라서 사용자는 요구사항 작성자가 아니라 문제와 경험을 설명하는 사람으로 볼 필요가 있다.

Agent는 다음 방식으로 도와야 한다.

- 한 번에 적은 수의 질문을 한다
- 선택지와 예시를 제시한다
- 이미 확인한 내용을 반복해서 묻지 않는다
- 전문 용어를 필요한 순간에 쉬운 말로 번역한다
- 중요한 결정에서만 사람의 선택을 요청한다
- 미확정 사항을 임의로 채우지 않는다

이 문제는 00의 Discovery, 01의 Human Decision, 02의 Human View, 07의 Context Presentation, 08의 Consultation Interface 전부에 영향을 준다.

---

# 11. 고객이 없는 1인 또는 3~5인 팀

프레임워크의 우선 적용 대상은 고객이 명확한 대기업 프로젝트가 아니라 다음과 같은 상황으로 정리되었다.

```text
고객 없음
확정 요구사항 없음
1인 또는 3~5인 소규모 팀
AI와 함께 사업 또는 프로젝트 아이템 탐색
```

이 상황에서는 Requirement부터 시작할 수 없다.

```text
Curiosity
→ Idea
→ Observation
→ Problem Discovery
→ Question Generation
→ Evidence
→ Vision
→ Requirement
```

그래서 01보다 앞에 00 Discovery Driven Development가 추가되었다.

---

# 12. 00 Discovery Driven Development

## 12.1 목적

무엇을 만들지 정하는 것이 아니라 해결할 가치가 있는 문제를 발견하고 검증한다.

## 12.2 흐름

```text
idea_space
→ problem_space
→ assumptions
→ evidence
→ opportunity
→ vision
→ decision
```

## 12.3 핵심 질문

- 누가 어떤 상황에서 불편을 겪는가
- 현재 어떤 대안을 사용하는가
- 그 대안은 왜 부족한가
- 문제의 빈도와 비용은 무엇인가
- 우리가 해결할 이유와 역량이 있는가
- 가장 작은 검증 방법은 무엇인가

## 12.4 판단권

AI는 문제 후보, 선택지, 조사와 추천을 제공할 수 있다. 그러나 어떤 문제를 선택하고 어떤 위험을 감수할지는 사람이 결정해야 한다.

권장 순서는 다음과 같다.

```text
AI가 선택지와 근거 제시
→ 역할을 맡은 사람이 선택
→ AI가 결정 결과 기록
```

AI가 `vision`이나 `decision`을 완성하고 사람이 통과만 시키면 사실상 AI가 결정한 것이 된다.

## 12.5 산출물

```yaml
idea_space.yaml
problem_space.yaml
assumptions.yaml
evidence.yaml
opportunity.yaml
vision.yaml
decision.yaml
```

## 12.6 앞으로의 비전

00은 단순 제품 기획 문서가 아니라 사용자가 질문을 만들기 어려울 때 AI가 사고를 보조하는 Discovery 환경으로 발전할 수 있다.

향후에는 다음을 검증해야 한다.

- 질문 피로를 줄이는 인터뷰 방식
- 사실, 가정과 희망의 자동 구분
- 외부 근거와 내부 판단의 연결
- AI 추천과 사람 선택의 분리
- 진행, 전환, 보류, 중단 결정을 위한 최소 기준

---

# 13. 01 AI Native SDLC

## 13.1 목적

검증된 문제를 설계, 개발, 검증, 배포, 운영과 학습이 가능한 생명주기로 전환한다.

## 13.2 10단계

10단계는 합치지 않고 그대로 유지한다.

```text
Vision
→ Specification
→ Domain Modeling
→ Architecture
→ Planning
→ Implementation
→ Verification
→ Release
→ Operation
→ Learning
```

단계가 10개라는 것이 Agent나 회의를 10개 만든다는 뜻은 아니다. 개념과 책임의 경계를 유지한다는 뜻이다.

## 13.3 역할 기반 결정권

승인자는 특정 사람 이름보다 역할로 정의한다.

```yaml
decision_authority:
  vision:
    decision_owner: product_owner
  architecture:
    decision_owner: tech_lead
  security:
    decision_owner: security_reviewer
  release:
    decision_owner: release_manager
```

혼자 수행할 때는 한 사람이 여러 역할을 겸한다. 그러나 기록상 역할은 구분한다.

또한 다음을 분리해야 한다.

```text
proposer
consulted
reviewer
decision_owner
recorder
challenger
```

## 13.4 위험별 검토

모든 산출물을 같은 깊이로 검토하면 승인 병목이 생긴다.

### 경량

문구, 스타일, 테스트 추가, 동작을 바꾸지 않는 리팩터링

```text
자동 테스트와 lint 중심
```

### 표준

기존 구조 안의 기능 추가와 변경

```text
별도 AI Session 리뷰
→ 작성자 확인
```

### 고위험

다음 질문 중 하나라도 예이면 고위험 후보다.

1. 되돌리기 어려운가
2. 영향 범위가 넓은가
3. 사용자, 돈, 보안에 영향을 주는가

예:

- DB 스키마와 데이터 마이그레이션
- 데이터 삭제와 개인정보 처리
- 인증과 권한
- 공개 API 변경
- 유료 서비스와 인프라 비용
- 운영 배포
- 서비스 경계와 핵심 기술 선택
- Agent 권한 변경

고위험 작업은 독립 AI 리뷰 후 작성자가 아닌 역할의 승인을 받는다. 혼자일 때는 새 Session, 시간 간격과 체크리스트를 최소 대체 통제로 사용한다.

## 13.5 독립 검증

같은 Session에서 AI가 자신이 구현한 결과를 검토하면 구현 과정의 가정과 자기합리화를 반복할 수 있다.

독립 Reviewer에게는 기본적으로 다음만 제공한다.

```text
Diff
수용 기준
관련 계약
테스트 결과
필수 안전 Context
```

## 13.6 앞으로의 비전

01은 AI 자동화 파이프라인이 아니라 사람의 결정과 AI 실행이 구분되는 개발 운영 체계로 발전해야 한다.

향후 검증 대상:

- 단계별 최소 산출물
- 위험 등급 자동 제안의 정확성
- 역할 기반 결정권의 팀 적용성
- 별도 Session 검증의 효과
- 운영 결과가 Discovery로 되돌아가는 학습 루프

---

# 14. 02 Project Knowledge Graph & Source of Truth

## 14.1 목적

프로젝트의 진실을 문서 더미가 아니라 상태, 관계, 결정 이력과 근거로 관리한다.

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

## 14.2 주요 파일

```text
current_state.yaml
domain_model.yaml
decision_index.yaml
system_graph view
traceability view
```

## 14.3 system_graph와 traceability

`system_graph`는 무엇이 무엇과 연결되어 있는지를 표현한다.

```text
주문 서비스 → depends_on → 결제 서비스
주문 API → uses → orders 테이블
```

`traceability`는 이것이 왜 존재하는지를 표현한다.

```text
문제 P-1
→ 요구사항 REQ-3
→ 결정 ADR-2
→ PR #45
→ Release 1.2
```

## 14.4 중앙 관계 파일의 문제

여러 사람이 각자의 AI로 하나의 큰 YAML을 수정하면 Git 충돌과 중복이 발생한다.

따라서 현재 추천 방향은 다음과 같다.

> 각 산출물이 자신이 직접 아는 관계를 로컬에서 선언하고, 스크립트가 관계를 모아 Graph와 Traceability View를 생성한다.

예:

```yaml
# ADR
id: ADR-2
decides:
  - REQ-3
```

```yaml
# PR metadata
refs:
  requirements:
    - REQ-3
  decisions:
    - ADR-2
  components:
    - payment-service
```

```yaml
# service metadata
id: payment-service
depends_on:
  - order-database
```

관계의 원본은 각 산출물이고, `system_graph`와 `traceability`는 자동 생성되는 파생 View다.

## 14.5 남은 문제

분산 선언만으로 모든 문제가 사라지지는 않는다.

- 관계 스키마를 누가 관리하는가
- 존재하지 않는 ID 참조를 어떻게 막는가
- 오래된 관계를 어떻게 삭제하는가
- 상충 관계를 어떻게 발견하는가
- 생성된 Graph가 최신인지 어떻게 보장하는가

따라서 CI에서 다음 검증이 필요하다.

```text
Schema Validation
Reference Integrity
Duplicate Relation Check
Replacement and Deletion Rules
Generated View Freshness
```

## 14.6 같은 PR에서 상태 갱신

코드 변경과 상태 갱신을 다른 PR로 나누면 일시적인 불일치가 발생한다.

```text
코드와 테스트 변경
관계 메타데이터
Current State Patch
필요한 문서 변경
```

을 가능한 한 같은 PR에서 검토한다.

같은 PR에 있다는 것이 같은 작성자가 모든 결정을 내린다는 뜻은 아니다. 필요한 Decision Owner와 Reviewer의 승인은 별도로 요구할 수 있다.

## 14.7 앞으로의 비전

02는 정적 문서 저장소가 아니라 분산 메타데이터에서 현재 상태와 관계 View를 생성하는 Knowledge System으로 발전할 수 있다.

향후 검증 대상:

- 분산 관계 선언의 실제 Git 충돌 감소 효과
- 상태와 코드의 자동 일치 검사
- Human View와 Agent View의 동기화
- 관계 삭제와 대체의 생명주기
- Graph 데이터베이스가 실제로 필요한 시점

---

# 15. 07 AI Native Context Architecture

## 15.1 목적

Agent에게 모든 문서를 주는 대신 작업에 필요한 최소한의 고신호 Context를 적시에 제공한다.

토큰 최소화는 단순 비용 절감이 아니다.

```text
정확성
비용
속도
추적성
보안
```

을 함께 최적화해야 한다.

## 15.2 Context 계층

```text
Core Context
Task Context
Evidence Context
Historical Context
```

권장 조회 순서:

```text
Context Manifest
→ Current State
→ Task Context
→ Related Graph Nodes
→ 필요한 Evidence
→ 필요할 때만 원문
```

## 15.3 Human View와 Agent View

```text
Human View = Markdown, 설명, 맥락, 다이어그램
Agent View = YAML, ID, 상태, 관계, 계약
```

두 View는 동일 ID를 공유하고 자동 검증해야 한다.

## 15.4 검토 깊이 차등

`task_context` 같은 실행 보조 산출물은 자동 검증을 통과하면 사람이 매번 읽지 않아도 된다.

`current_state`는 전체가 아니라 변경 Diff와 근거를 본다.

Vision, Architecture Decision, 보안 정책, 운영 배포 같은 고위험 판단 산출물은 사람이 직접 선택하거나 승인한다.

## 15.5 도구 독립성

핵심 문서에는 특정 제품에 의존하는 사용법을 넣지 않는다.

```text
본문 = 개념, 역할, 계약, 검증 규칙
부록 = Claude Code, Codex, Cursor, GitHub Copilot 구현법
```

도구가 바뀌어도 프레임워크 본문은 유지되어야 한다.

## 15.6 앞으로의 비전

07은 문서 검색 시스템이 아니라 역할과 작업에 따라 Context를 동적으로 조립하는 계층으로 발전할 수 있다.

향후 검증 대상:

- 토큰 감소와 정확성 사이의 균형
- 중요한 예외가 요약에서 손실되는 문제
- 역할별 Context View의 효과
- MCP와 외부 검색 도구의 최소 구성을 정하는 방법
- Context Manifest 자동 생성과 검증

---

# 16. 08 AI Native Agent Organization

## 16.1 목적

Agent 이름을 많이 만드는 것이 아니라 역할, 책임, 입력, 출력, 권한, Context, 승인과 중단 조건을 계약으로 정의한다.

## 16.2 기본 원칙

```text
예측 가능한 절차
→ 일반 코드 또는 Workflow

판단과 불확실성이 필요한 업무
→ Agent
```

단일 Agent로 충분하다면 Multi-Agent를 만들지 않는다.

## 16.3 역할 체계

```text
Discovery
Question / Consultation
Documentation
DDD
Architecture
Planning
Coding
QA
Deployment
Operations
Knowledge
Orchestrator
```

## 16.4 Agent 계약

```yaml
agent:
  id:
  purpose:
  inputs:
  outputs:
  tools:
  permissions:
  context_budget:
  decision_rights:
  approval:
  stop_conditions:
  evaluation:
```

## 16.5 AI의 제안과 사람의 결정

AI는 선택지, 트레이드오프와 추천을 제시한다. Decision Owner 역할이 실제 선택을 한다. AI는 그 선택을 기록한다.

```text
AI 분석과 추천
→ 역할 기반 사람의 선택
→ AI의 결정 기록
```

AI가 결론을 만들고 사람이 통과만 시키는 구조는 피한다.

## 16.6 별도 Session Reviewer

작성 Agent와 Reviewer Agent는 가능한 한 Context를 분리한다.

고위험 작업은 작성자가 아닌 팀원 역할이 승인한다. 1인 프로젝트에서는 새로운 Session과 시간 간격을 이용한다.

## 16.7 소규모 팀 MVP

처음부터 모든 역할을 별도 Agent로 만들 필요는 없다.

```text
Discovery / Consultation
Builder
Reviewer
Knowledge
```

네 논리적 역할로 시작할 수 있다. 한 모델이 여러 역할을 수행하더라도 Session, 권한과 Context는 분리한다.

## 16.8 앞으로의 비전

08은 코딩 Agent 집합이 아니라 사람과 Agent의 결정권과 책임을 포함하는 운영 모델로 발전할 수 있다.

향후 검증 대상:

- 역할 분리가 필요한 임계 조건
- Multi-Agent가 실제로 품질을 높이는 작업 유형
- Agent 간 무한 위임 방지
- 역할별 최소 권한
- AI 추천과 사람 결정의 추적 기록
- 여러 팀원이 각자 Agent를 사용할 때의 충돌 해결

---

# 17. 개발자의 주요 착각

이 프레임워크는 이상적인 방식뿐 아니라 실패 가능성도 함께 기록해야 한다.

- AI가 코딩을 잘하니 설계가 덜 중요하다
- 문서를 많이 넣으면 AI가 더 잘 이해한다
- ADR을 많이 남기면 자동으로 지식 체계가 된다
- AI가 요구사항의 빈칸을 올바르게 채운다
- 테스트 통과가 사용자 가치와 운영 안전을 증명한다
- Agent 수가 많으면 품질이 높아진다
- Knowledge Agent가 쓴 상태는 자동으로 진실이다
- 토큰을 줄이면 무조건 좋은 Context Architecture다
- 사람이 승인 버튼을 누르면 사람의 결정이다
- 모든 AI 산출물을 같은 깊이로 읽어야 안전하다

이 착각들을 방지하려면 다음 분리가 필요하다.

```text
AI의 제안과 사람의 결정
원본과 파생 View
Current State와 Decision History
실행 보조 산출물과 판단 산출물
작성 Session과 검증 Session
방법론 본문과 도구별 부록
```

---

# 18. 현재까지의 합의 상태

## 합의된 방향

- 도구 의존 내용은 부록으로 분리한다
- 00은 `idea_space`부터 `decision`까지 순서대로 명세한다
- 01의 10단계는 합치지 않는다
- 승인자와 Decision Owner는 사람 이름보다 역할로 정의한다
- 한 사람이 여러 역할을 겸할 수 있지만 역할 기록은 분리한다
- 관계는 각 산출물 근처에서 분산 선언한다
- Graph와 Traceability는 가능한 한 자동 생성 View로 취급한다
- 위험 등급에 따라 검증 깊이를 다르게 한다
- 고위험 작업은 독립 Session과 다른 역할의 검토를 사용한다
- 코드와 관련 상태 갱신은 가능한 한 같은 PR에서 검토한다

## 제안 단계이며 추가 검증이 필요한 방향

- 분산 관계 선언의 정확한 공통 스키마
- 위험 등급을 정하는 자동 규칙과 하향 승인 절차
- 1인 프로젝트에서 고위험 검토를 대체할 충분한 통제
- 생성 Graph의 저장 또는 동적 생성 여부
- Markdown과 YAML 이중 유지의 비용
- Knowledge Agent가 상태 갱신 후보를 만드는 정확성

## 아직 열려 있는 질문

- Vision의 최종 Decision Owner는 누구인가
- 제품, 기술, 보안, 배포 결정 사이의 충돌은 누가 해결하는가
- 관계 삭제와 대체를 어떻게 표현하는가
- 상태와 코드가 불일치하면 어느 수준에서 CI를 실패시키는가
- 어떤 시점에 Jira, Backstage, Graph DB와 MCP를 도입하는가
- AI의 기억과 저장소의 공식 기록 중 무엇을 우선하는가

---

# 19. 전체 프레임워크의 관계

```text
00 = 무엇을 왜 만들 것인가
01 = 어떻게 만들고 운영하며 학습할 것인가
02 = 프로젝트의 진실과 관계는 무엇인가
07 = 어떤 Context를 누구에게 얼마나 제공할 것인가
08 = 누가 어떤 책임, 권한과 검증 방식으로 일할 것인가
```

전체 순환:

```text
사람의 경험과 관찰
        ↓
00 문제 발견과 선택
        ↓
01 설계, 개발, 검증, 배포, 운영과 학습
        ↓
02 상태, 관계, 결정 이력과 근거 축적
        ↓
07 역할과 작업에 맞는 최소 Context 구성
        ↓
08 역할별 Agent 수행과 독립 검증
        ↓
코드, 테스트, 릴리스와 운영 결과
        ↓
Knowledge Agent의 상태 갱신 제안
        ↓
역할 기반 검증과 같은 PR에서 병합
        ↓
새로운 관찰과 문제
        ↓
다시 00
```

---

# 20. 소규모 팀에서의 현실적인 시작점

전체 구조를 처음부터 구축하지 않는다.

## 최소 사람용 문서

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
자동 테스트와 CI
역할별 AI Session
```

검색, 작업 추적, 서비스 수와 팀 충돌이 실제로 커질 때 Jira, 서비스 카탈로그, Graph Store와 MCP를 단계적으로 추가한다.

---

# 21. 앞으로의 비전

이 프레임워크의 장기 비전은 AI가 코드를 대신 작성하는 환경을 만드는 데 그치지 않는다.

## 21.1 질문을 요구하는 AI에서 질문을 함께 만드는 AI로

사용자에게 완성된 질문을 요구하지 않는다. 경험과 불편을 바탕으로 AI가 질문 후보를 만들고 사용자는 중요한 선택에 집중한다.

## 21.2 문서를 쌓는 저장소에서 현재 상태를 유지하는 지식 시스템으로

과거 문서는 이력으로 보존하되, Current State와 관계 View를 작고 명확하게 유지한다.

## 21.3 하나의 거대한 Agent에서 역할 기반 조직으로

업무와 위험에 따라 역할, Context와 권한을 분리한다. 그러나 필요 이상의 Agent는 만들지 않는다.

## 21.4 인간 승인에서 인간 결정으로

사람은 AI가 만든 결론을 통과시키는 존재가 아니라 선택지를 비교하고 위험을 수용하는 Decision Owner가 된다.

## 21.5 모든 것을 읽는 검토에서 위험 기반 검토로

경량 산출물은 자동 검사하고, 상태 변경은 Diff를 검토하며, 고위험 판단은 사람이 직접 결정한다.

## 21.6 중앙 YAML 편집에서 분산 관계 선언과 자동 View 생성으로

각 산출물이 자신이 아는 관계를 기록하고, 시스템이 이를 수집해 Graph와 Traceability를 생성한다.

## 21.7 코드 중심 자산에서 문제와 학습의 연결 자산으로

장기적으로 보존할 자산은 코드만이 아니다.

```text
Problem
Vision
Requirement
Domain
Decision
Current State
Relationships
Context
Agent Contract
Code
Release
Operation
Learning
```

이 연결 전체가 프로젝트의 자산이 된다.

---

# 22. 다음 실험 과제

1. 00의 `idea_space` 명세부터 한 단계씩 정의한다
2. 역할 기반 Decision Authority 파일을 만든다
3. 관계 분산 선언의 최소 스키마를 만든다
4. 참조 무결성을 검사하는 CI 규칙을 만든다
5. 경량, 표준, 고위험 Review Policy를 만든다
6. 별도 Reviewer Session 실험을 진행한다
7. 같은 PR에서 코드와 상태 Patch를 검토한다
8. 소규모 실제 프로젝트 하나에 최소 구조를 적용한다
9. 토큰 비용, 재작업 수, 상태 불일치와 검토 시간을 측정한다
10. 결과를 다시 00의 문제와 가정에 환류한다

---

# 23. 최종 정의

> AI Native Development Framework는 사람이 완성된 요구사항을 AI에게 전달하고 결과를 승인하는 방식이 아니다. 사람이 경험, 가치 판단과 책임을 제공하고, AI가 필요한 질문, 선택지와 실행 결과를 만들며, 역할을 맡은 사람이 실제 결정을 내리고, 구조화된 Agent 조직이 이를 구현하고 독립적으로 검증하고, 프로젝트의 현재 상태와 관계를 지속적으로 갱신하는 학습형 개발 방식이다.

이 문서는 최종 정답이 아니라 다음 AI Agent 및 팀원과 대화를 이어가기 위한 공통 출발점이다. 새로운 제안은 기존 논의의 배경, 현재 합의, 미해결 질문과 장기 비전을 모두 고려해 평가해야 한다.

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
