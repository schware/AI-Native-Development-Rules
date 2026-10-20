# 07. AI Native Context Architecture

## 1. 이 문서가 생긴 대화의 흐름

ADR과 문서가 늘어나자 단순 상태 표시만으로는 토큰 문제를 해결하지 못한다는 점이 드러났다. Multi-Agent 구조에서는 각 Agent가 같은 문서를 반복해서 읽어 Context 비용과 불일치가 더 커진다.

또한 문서를 모두 넣는다고 이해가 좋아지는 것이 아니었다. 오래된 정보, 중복과 대용량 도구 결과가 중요한 정보를 흐릴 수 있었다.

그래서 다음 원칙이 생겼다.

> 모든 문서를 읽히지 말고, 역할과 작업에 필요한 최소한의 고신호 Context를 적시에 제공한다.

이것이 07의 출발점이다.

## 2. 목적

토큰을 줄이는 것만이 아니라 정확성, 비용, 속도, 추적성과 보안을 함께 최적화한다.

## 3. Context 계층

### Core Context

프로젝트 목표, 역할, 권한, 핵심 제약과 Current State

### Task Context

이번 작업의 범위, 수용 기준, 수정 가능 영역, 금지 영역과 검증 방법

### Evidence Context

필요한 ADR, 코드, 이슈와 운영 데이터의 선택된 부분

### Historical Context

회의 원문과 과거 문서처럼 필요한 경우에만 조회하는 자료

## 4. 권장 로딩 순서

```text
Context Manifest
→ Current State
→ Task Context
→ Related Graph Nodes
→ 필요한 Evidence
→ 필요할 때만 원문
```

## 5. 예시

```yaml
task:
  id: TASK-142
  goal: 주문 취소 API 추가
  acceptance_criteria:
    - 결제 완료 전 주문 취소 가능
    - 취소 이력 저장
    - 기존 환불 기능 변경 금지

context:
  required:
    - REQ-032
    - BC-ORDER
    - API-ORDER
    - ADR-017

permissions:
  write_paths:
    - src/order/**
    - tests/order/**
  forbidden_paths:
    - src/payment/**

budget:
  max_documents: 6
  load_full_history: false
```

## 6. Human View와 Agent View

Markdown은 설명과 토론을 위한 형식이고 YAML은 상태와 계약을 압축하기 위한 형식이다.

```text
Human View + Agent View
```

두 View는 동일 ID를 사용하고 자동 검증한다. YAML은 인간 검토를 없애기 위한 수단이 아니며 Markdown을 대체하지 않는다.

## 7. 산출물별 검토 깊이

### 실행 보조 산출물

`task_context`, 검색 결과, 임시 계획

```text
스키마와 자동 검사 중심
```

### 상태 변경 산출물

`current_state`, 관계 메타데이터

```text
전체 파일보다 Diff, 영향 범위와 근거 검토
```

### 판단 산출물

Vision, Architecture Decision, 보안 정책, 운영 배포

```text
AI가 선택지와 근거 제시
→ 사람 Decision Owner가 선택
```

## 8. 토큰 최소화 원칙

- 전체 문서보다 ID와 요약을 먼저 사용한다.
- 역할별 Context View를 제공한다.
- 재조회 가능한 대용량 도구 결과를 장기 Context에 유지하지 않는다.
- 중복과 오래된 정보를 제거한다.
- 요약에 원문 ID, 생성 시각, 생성 주체와 신뢰 수준을 기록한다.
- 비용 절감이 정확성과 추적성을 훼손하지 않는지 평가한다.

## 9. 도구 독립성

본문에는 특정 도구 사용법을 넣지 않는다.

```text
본문 = 개념, 역할, 계약, 정책
부록 = Claude Code, Codex, Cursor, GitHub Copilot 구현
```

도구를 교체해도 본문은 유지되어야 한다.

## 10. 단계적 Tooling

### 초기

```text
GitHub
Markdown
YAML
CI
```

### 필요 발생 후

```text
작업 추적 도구
서비스 카탈로그
Graph Store
MCP 또는 API 통합
```

도구를 먼저 도입하지 않고 실제 검색, 충돌, 권한과 규모 문제가 생길 때 추가한다.

## 11. 개발자의 착각과 실패 패턴

- 모든 문서를 넣으면 AI가 더 잘 이해한다고 생각한다.
- 토큰을 줄이면 무조건 좋은 Context라고 생각한다.
- 요약에서 중요한 예외가 사라지지 않는다고 가정한다.
- 모든 Agent에게 동일 Context를 제공한다.
- 도구 출력을 계속 누적한다.
- Context Cache가 항상 최신이라고 가정한다.
- 제품 기능을 방법론 본문에 결합한다.

## 12. 현재 합의와 미해결 사항

### 합의

- State First와 Just-in-Time Retrieval을 기본으로 한다.
- Markdown과 YAML의 이중 View를 유지한다.
- 산출물과 위험에 따라 검토 깊이를 다르게 한다.
- 도구 의존 내용은 부록으로 분리한다.

### 미해결

- 역할별 Context Budget
- 요약 손실 평가 방법
- Context Manifest 자동 생성 규칙
- MCP 도구의 최소 구성과 보안 경계
- 이중 View 유지 비용

## 13. 앞으로의 비전

07은 문서 검색에서 역할과 작업에 맞는 Context를 동적으로 조립하는 계층으로 발전한다. 장기적으로는 Agent가 필요한 정보를 스스로 찾되, 권한, 비용, 원문 근거와 Human Explainability가 함께 보장되어야 한다.

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
