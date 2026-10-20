# 00. Discovery Driven Development

## 1. 이 문서가 생긴 대화의 흐름

처음에는 정리된 문서를 AI Agent에게 전달하면 Agent가 개발할 수 있다고 생각했다.

```text
문서 정리
→ 요구사항
→ AI Agent
→ 구현
```

하지만 이 흐름은 고객이나 명확한 요구사항이 이미 존재한다는 가정을 갖고 있었다. 실제로 상정한 환경은 고객이 없고, 혼자 또는 3~5명이 무엇을 만들지부터 찾아야 하는 상황이었다.

더 큰 문제는 사람이 좋은 질문을 만들기 어려울 수 있다는 점이었다. AI에게 계속 질문하라고 요구하는 방식은 다음과 같은 피로를 만든다.

```text
막연한 생각
→ 무엇을 질문해야 할지 모름
→ AI의 반복 질문
→ 결정 피로
→ 대화 중단 또는 성급한 동의
```

이 문제 때문에 Requirement보다 앞에 Discovery가 필요해졌다.

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

00은 이 전환을 담당한다.

## 2. 목적

무엇을 만들지 빠르게 정하는 것이 아니라, 해결할 가치가 있는 문제가 실제로 존재하는지 확인한다.

AI는 사용자의 생각을 대신 결정하지 않는다. AI의 역할은 문제 후보, 질문, 대안과 근거를 제공하는 것이며, 어떤 문제를 선택할지는 역할을 맡은 사람이 결정한다.

## 3. 기본 흐름

현재 합의된 순서대로 하나씩 명세한다.

```text
idea_space
→ problem_space
→ assumptions
→ evidence
→ opportunity
→ vision
→ decision
```

각 단계마다 다음을 정의한다.

```text
목적
입력
필수 필드
선택 필드
AI가 제안할 항목
사람이 결정할 항목
검증 규칙
다음 단계 진입 조건
```

## 4. 단계별 의미

### 4.1 idea_space

막연한 관심, 불편, 반복 작업과 관찰을 보존한다. 아직 문제나 기능으로 단정하지 않는다.

```yaml
ideas:
  - id: IDEA-001
    observation: AI와 개발 대화를 이어가면 합의 배경이 사라진다
    source: personal_experience
    status: exploring
```

### 4.2 problem_space

해결책 표현을 제거하고 누가, 어떤 상황에서, 무엇 때문에 어려운지 정리한다.

```yaml
problems:
  - id: PROB-001
    actor: small_ai_native_team
    situation: framework discussion across sessions
    pain: rationale and prior agreements are lost
    current_alternative: manually reread conversations
```

### 4.3 assumptions

사실, 해석, 가정과 희망을 구분한다.

```yaml
assumptions:
  - id: ASM-001
    statement: rationale-rich documents reduce repeated discussion
    type: hypothesis
    validation_status: untested
```

### 4.4 evidence

외부 자료, 인터뷰, 실험, 로그와 대화 기록을 연결한다. AI가 만든 요약과 원자료를 구분한다.

### 4.5 opportunity

문제의 가치, 실행 가능성, 전략적 적합성과 최소 검증 방법을 정리한다.

### 4.6 vision

AI가 Vision을 완성하고 사람이 승인만 해서는 안 된다.

권장 순서:

```text
AI가 Vision 선택지와 차이 제시
→ Product Owner 역할이 선택
→ AI가 선택 결과 기록
```

### 4.7 decision

`go`, `pivot`, `hold`, `stop` 중 하나를 사람이 선택하고 AI가 근거와 함께 기록한다.

## 5. Agent 역할

- Discovery Agent: 관찰을 문제 후보로 변환한다.
- Research Agent: 기존 대안과 외부 근거를 조사한다.
- Question Agent: 사용자가 만들지 못한 질문을 단계적으로 제시한다.
- Red-Team Agent: 기술 편향, 확인 편향과 근거 없는 수요를 공격한다.
- Documentation Agent: 사람의 선택을 구조화된 파일로 기록한다.

## 6. 사용자 접근성 원칙

- 한 번에 적은 수의 질문만 한다.
- 가능한 경우 선택지와 예시를 제시한다.
- 이미 확인한 답을 반복해서 묻지 않는다.
- 전문 용어는 필요한 순간에 번역한다.
- 미확정 답을 임의로 채우지 않는다.
- 사용자는 요구사항 작성자가 아니라 자신의 경험과 문제를 설명하는 사람으로 본다.

## 7. 개발자의 착각과 실패 패턴

- 흥미로운 기술을 문제로 착각한다.
- 자신의 불편을 외부 검증 없이 시장 문제로 확대한다.
- AI가 제시한 수치와 사례를 근거 없이 사실로 취급한다.
- AI가 작성한 Vision을 사람이 통과시키면 인간 결정이라고 생각한다.
- 질문을 많이 할수록 Discovery 품질이 높아진다고 생각한다.

## 8. 종료 조건

- 대상 사용자 또는 행위자가 정의되어 있다.
- 문제 상황과 현재 대안이 기록되어 있다.
- 사실과 가정이 분리되어 있다.
- 가장 위험한 가정과 다음 검증 방법이 있다.
- Decision Owner가 진행 방향을 선택했다.

## 9. 현재 합의와 미해결 사항

### 합의

- `idea_space`부터 `decision`까지 순서대로 명세한다.
- AI의 추천과 사람의 선택을 분리한다.
- 도구별 구현 방식은 부록으로 분리한다.

### 미해결

- Vision의 최종 Decision Owner 역할
- 질문 피로를 측정하는 기준
- Evidence의 최소 신뢰 등급
- `go`, `pivot`, `hold`, `stop`을 위한 최소 Gate

## 10. 앞으로의 비전

00은 제품 기획 템플릿을 넘어 사용자가 질문을 만들지 못할 때 AI가 사고를 보조하는 Discovery 환경으로 발전한다. 장기적으로는 대화의 양이 아니라 더 나은 문제 선택, 더 적은 불필요한 구현과 명확한 인간 결정을 성과로 평가한다.

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
