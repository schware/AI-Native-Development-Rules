# Framework Decision Log

## 이 문서

- 프레임워크 자체에 대한 결정 이력이다. 02의 Decision History에 해당한다.
- **결정 상세는 추가만 한다.** 기존 항목은 고치지 않고, 결정이 바뀌면 새 항목을 만들어 `replaces`로 연결한다.
- **결정 요약, 합의된 규칙, 미확인 draft, 미해결은 현재 상태다.** 결정이 추가될 때마다 함께 갱신한다.
- Claude Code memory에만 있던 합의를 저장소로 옮긴 것이다. 원칙: 저장소에 기록된 것만 결정으로 인정한다 (DEC-013).
- 포맷은 임시다. 결정 기록 포맷이 확정되면 그 형식으로 바꾼다.

**표기**

- 채택 방식: `AI 추천 그대로` / `AI 추천 수정` / `사람 제안`
- 이유 작성자:
  - `Sun&Moon(생각)`, `Sun&Moon(질문과 생각)`: 문서에 직접 작성
  - `Sun&Moon (발언 요약)`: 대화 중 발언을 Claude Code가 요약
  - `claude_code (draft)`: 확인 필요
  - `claude_code (draft, 확인: 이름 날짜)`: 확인 완료
  - `claude_code (참고)`: 질문에 대한 답변이나 설명. 이유가 아니므로 미결정 집계에 넣지 않는다.
- 확인 판정: AI draft 아래에 Sun&Moon이 직접 글을 남긴 결정은 확인된 것으로 본다. 그 글에 담긴 질문은 "미해결"에서 따로 관리한다.
- v03 반영: `반영됨` / `부분` / `미반영`

---

## 배경: 왜 이 작업을 하는가

**겪은 문제**

```text
AI가 답 하나를 완성된 형태로 제시
→ 대안을 본 적이 없으니 정답처럼 보여 넘어감
→ 그 위에 계속 쌓음
→ 나중에 잘못이 보임 → 고치면 리스크 → 선택해서 수정
→ 또 다른 리스크 → 반복 → 결국 전체 다시 만들기

기록은 포맷 없이 AI가 정리
→ 다시 읽어도 파악이 안 됨 → 다시 보기 포기
→ 결과물 없이 시간과 토큰만 소모, "공부했다"는 착각
```

**핵심 진단**: "그냥 넘긴 것"이 문제가 아니라, **그 자리에 선택이 있었다는 것 자체를 보지 못한 것**이 문제다. 설계에 투자해야 할 대상은 문서의 양이 아니라 **선택을 드러내는 약속(포맷)**이다.

**목표**

- 가장 큰 목표는 **경계를 만드는 작업**이다. AI 제안과 사람 결정, 역할 사이의 결정권, 위험 등급, 원본과 파생물 사이에 경계를 세운다.
- 팀장, PM, PL이 되었을 때 AI Agent를 활용할 수 있는 사람으로 성장한다.

---

## 결정 요약

| ID | 결정 | 채택 방식 | 이유 작성자 | v03 |
|---|---|---|---|---|
| DEC-001 | 작업 기간 관리 도구는 Jira | 사람 제안 | claude_code (draft) + Sun&Moon(생각) | 미반영 |
| DEC-002 | 대상은 3~5인 팀 | 사람 제안 | Sun&Moon (발언 요약) | 부분 |
| DEC-003 | 기준 문서는 v03 | AI 추천 그대로 | claude_code (draft) + Sun&Moon(생각) | — |
| DEC-004 | 본문은 도구 중립, 도구별 내용은 부록 | AI 추천 그대로 | Sun&Moon (발언 요약) | 반영됨 |
| DEC-005 | 00 산출물 7개를 모두 명세 | 사람 제안 | Sun&Moon (발언 요약) + Sun&Moon(생각) | 반영됨 |
| DEC-006 | 01의 10단계 유지 | 사람 제안 | Sun&Moon (발언 요약) + Sun&Moon(생각) | 반영됨 |
| DEC-007 | 규칙 강도 표기 (MUST/SHOULD/MAY/MUST NOT)<br>*언어 부분은 DEC-018이 대체* | AI 추천 수정 | Sun&Moon (발언 요약) | 미반영 |
| DEC-008 | 위험 등급 (low/medium/high)<br>*표기는 DEC-020이 대체* | AI 추천 그대로 | claude_code (draft) + Sun&Moon(생각) | 부분 |
| DEC-009 | 상태 갱신은 같은 PR에서 | AI 추천 그대로 | claude_code (draft) + Sun&Moon(생각) | 반영됨 |
| DEC-010 | 관계는 분산 선언, Graph는 필요할 때 생성 | AI 추천 그대로 | Sun&Moon (발언 요약) | 부분 |
| DEC-011 | 기간 단위 운영 (시작할 때 계획, 마칠 때 다시 보기)<br>*기간 체계는 DEC-021* | 사람 제안 | claude_code (draft) + Sun&Moon(생각) | 미반영 |
| DEC-012 | 결정 기록 요구사항 R1~R6<br>*R2와 R4는 DEC-017, DEC-019가 보완* | AI 추천 수정 | Sun&Moon (발언 요약) | 부분 |
| DEC-013 | 저장소에 기록된 것만 결정으로 인정 | AI 추천 그대로 | Sun&Moon (발언 요약) | 미반영 |
| DEC-014 | 원본 경계: 작업 상태는 Jira, 결정과 설계는 저장소 | AI 추천 그대로 | claude_code (draft) + Sun&Moon(생각) | 미반영 |
| DEC-015 | 설계 변경 시 결정 기록 필수 | 사람 제안 | Sun&Moon (발언 요약) | 미반영 |
| DEC-016 | Verification 범위: 자동 검사와 체크리스트 | AI 추천 그대로 | claude_code (draft) + Sun&Moon(질문과 생각) | 미반영 |
| DEC-017 | high 결정은 사람이 확인해야 진행 | AI 추천 수정 | claude_code (draft) + Sun&Moon(생각) | 미반영 |
| DEC-018 | 규칙 문장은 영어가 원본 | 사람 제안 | Sun&Moon (발언 요약) | 미반영 |
| DEC-019 | 확인되지 않은 draft는 미결정으로 셈 | AI 추천 수정 | claude_code (draft) + Sun&Moon(생각) | 미반영 |
| DEC-020 | 위험 등급은 영어로만 표시 | 사람 제안 |  Sun&Moon (결정) | 반영 |
| DEC-021 | 기간 체계: Weekly / Monthly / Quarter / Half / Year | 사람 제안 | Sun&Moon(생각) | 미반영 |
| DEC-022 | GitHub 공개 저장소 `AI-Native-Development-Rules` | 사람 제안 | Sun&Moon (발언 요약) | — |

---

## 결정 상세

### DEC-001 작업 기간 관리 도구는 Jira

- **결정**: 기간 단위 운영(DEC-011)의 도구로 Jira를 사용한다.
- **AI 추천**: GitHub Projects. 이미 쓰는 GitHub 안에서 해결되고, 작업 정보가 두 곳으로 나뉘지 않는다.
- **채택**: 사람 제안 (추천과 다름)
- **이유**: PM/PL 역량을 쌓고 팀 확장에 대비해 업계 표준 도구를 익힌다.  — *claude_code (draft)*
  - 추가적인 이유는 Github Projects 를 사용해서 느낀 점은 PR 중심적으로 동작 하고 일정이나 진행 사항 보다는 Commit 을 목표로 해서 내가 막힌 것이 있을때.. 무엇 때문인지 찾을 수 없다는 느낌이 강해서 Jira로 가려고 합니다. — *Sun&Moon(생각)*
- **영향**: v03 07 §10의 "도구는 필요할 때 도입" 원칙에 예외가 생긴다.

### DEC-002 대상은 3~5인 팀

- **결정**: 3~5인 팀을 기준으로 설계한다. 1인은 한 사람이 여러 역할을 겸하는 특수한 경우로 보고, 대체 통제를 따로 적는다.
- **AI 추천**: 1인 팀을 위한 최소 프로필
- **채택**: 사람 제안 (추천과 다름)
- **이유**: 1인 기준으로 만들면 쓰다가 결국 한계를 느낀다. AI를 하는 이유도 팀원을 만들고 싶어서다. — *Sun&Moon (발언 요약)*
- **결과**: 승인자와 Decision Owner를 사람 이름이 아니라 역할로 정의한다 (v03 01 §6).

### DEC-003 기준 문서는 v03

- **결정**: `ai-native-development-framework-v03/`을 기준으로 삼는다. 예전 Human/Agent 세트와 evolution 문서는 `ai-native-development-framework-markdown-sets/`에 이력으로 보관한다.
- **채택**: AI 추천 그대로
- **이유**: 협의한 내용이 대부분 반영된 최신본이다. — *claude_code (draft)*
  - 추가 내용을 정리 했고 그리고 최소한 내가 생각한 문장이 많이 포함되어서 이것으로 하려고 합니다.앞으로 제 생각이 더 들어간 문서를 만들기 위해서 Decision-log도 만드는 것입니다.  — *Sun&Moon(생각)*

### DEC-004 본문은 도구 중립, 도구별 내용은 부록

- **결정**: 본문에는 개념, 역할, 계약, 정책만 둔다. 도구 사용법은 부록에 둔다. 현재 부록은 Claude Code만 있다.
- **채택**: AI 추천 그대로
- **이유**: Codex, Cursor 도입을 아직 고민 중이다. 도구를 바꿔도 본문은 그대로 유지되어야 한다. — *Sun&Moon (발언 요약)*

### DEC-005 00 산출물 7개를 모두 명세

- **결정**: `idea_space`, `problem_space`, `assumptions`, `evidence`, `opportunity`, `vision`, `decision`을 순서대로 하나씩 명세한다. 줄일 부분은 명세한 뒤에 협의한다.
- **AI 추천**: §19의 최소 세트부터 명세
- **채택**: 사람 제안 (추천과 다름)
- **이유**: 무엇을 줄일지는 전체를 본 뒤에 정한다. 명세 자체가 큰 작업이라 느려지는 것은 감수한다. — *Sun&Moon (발언 요약)*
  - 이부분에 명세표를 제가 만들어서 최소한의 규칙을 정해야 합니다. 많은 검색과 도움이 필요 합니다. — *Sun&Moon(생각)*

### DEC-006 01의 10단계 유지

- **결정**: Vision부터 Learning까지 10단계를 합치지 않는다.
- **AI 추천**: 1인 팀이면 4~5단계로 묶음
- **채택**: 사람 제안 (추천과 다름)
- **이유**: 팀을 기준으로 한다 (DEC-002). — *Sun&Moon (발언 요약)*
  - 혼자서 하게 되면 결국 .. 합치면서 기억 못하게 되면 문제점이 지속적으로 나타난다. — *Sun&Moon(생각)*

### DEC-007 규칙 강도 표기

- **결정**:
  - 규칙 강도는 `[MUST]`, `[SHOULD]`, `[MAY]`, `[MUST NOT]`으로 표기한다 (RFC 2119).
  - `[MUST]` 규칙에는 `Verification`(확인 방법)을 함께 적는다. 확인할 수 없는 규칙은 MUST가 될 수 없다.
  - 규칙 문장은 한국어로 쓰고 괄호 안에 영어를 함께 적는다. 긴 문장은 한국어로만 쓰고, 무리하게 번역하지 않는다.
- **AI 추천**: 영어 키워드만 사용
- **채택**: AI 추천 수정 (문장을 두 언어로 쓰는 것은 사람 제안)
- **이유**: 영어에 익숙해지고 싶다. 영어 키워드는 AI가 표준 의미로 정확하게 해석한다. — *Sun&Moon (발언 요약)*
- **참고**: RFC 2119의 SHOULD는 "타당한 이유가 있으면 지키지 않아도 되지만, 그 영향은 이해해야 한다"는 뜻이다. R2(이유를 쓰지 않아도 진행을 막지 않음)와 의미가 같다.

### DEC-008 위험 등급

- **결정**: `risk_level`은 `low`(경량), `medium`(표준), `high`(고위험) 세 가지다. 아래 질문 중 하나라도 "예"이면 high 후보로 본다.
  1. 되돌리기 어려운가?
  2. 영향 범위가 넓은가?
  3. 사용자, 돈, 보안에 영향을 주는가?
- **대표적인 high 항목**: DB 스키마와 마이그레이션, 데이터 삭제와 개인정보, 인증과 권한, 공개 API 계약, 비용, 운영 배포, 서비스 경계와 핵심 기술 선택, Agent 권한 변경
- **채택**: AI 추천 그대로
- **이유**: 목록으로 정해 두면 AI가 작업을 시작할 때 스스로 등급을 판정할 수 있다. — *claude_code (draft)*
  - 위험도에 대해서 어떤 문서에 지정하는지 확인이 필요하다. 그래야지 위험 등급 설정에 대해서 명확하게 알 수 있을 것 같다.  — *Sun&Moon(생각)*
  - 등급 기준은 v03 01 §7과 이 결정에 있다. 작업과 결정마다 등급을 매기는 위치는 아직 정하지 않았다 (미해결 참고). — *claude_code (참고)*
- **v03**: 01 §7에 한국어 용어로 반영되어 있다. 영어로만 표시 한다. (→ DEC-020)

### DEC-009 상태 갱신은 같은 PR에서

- **결정**: 코드, 테스트, 관계 메타데이터, Current State 변경분을 같은 PR에서 함께 검토한다.
- **채택**: AI 추천 그대로
- **이유**: 갱신을 별도 단계로 분리하면 결국 끊긴다. — *claude_code (draft)*
  - 모든 선택은 once 로 할 계획이다. 귀찮아도 once 하려고 한다. 아니에요 always once 라는 선택 항목을 이야기 하는 것이에요  — *Sun&Moon(생각)*
  - once와 always는 AI 도구가 권한을 요청할 때 고르는 항목이다. 귀찮아도 매번 "이번만 허용(once)"을 고르고, "항상 허용(always)"은 쓰지 않는다는 뜻이다. — *claude_code (참고)*

### DEC-010 관계는 분산 선언, Graph는 필요할 때 생성

- **결정**:
  - 관계의 원본은 각 산출물이다 (ADR의 `decides`, PR의 `refs` 등).
  - Graph는 스크립트가 필요할 때 생성하며, 파일로 저장하지 않는다.
  - 주간이나 월간 Graph는 PM/PL이 보는 보고서로만 만들고, AI는 이를 읽지 않는다.
- **채택**: AI 추천 그대로
- **이유**:
- 한 달 동안 작업하다 보면 "전에 결정했다"는 말을 듣고도 그 근거를 찾지 못한다. Graph는 그 근거를 따라가는 길이다. — *Sun&Moon (발언 요약)*
- Graph 에 대해서 파일이 생성시 자동으로 update 하는 부분에 대해서 다시 한번 검토를 요청해요. 저희가 대화를 진행할때 이 부분에 대해서 주기에 대한 부분을 정리 한것으로 판단 했는데 아닌가봐요 확인이 필요 합니다. 이렇게 문서의 확인 요청이 필요할때 어떻게 처리 해야 할까요? 
- **추가 근거**: 주기적으로 저장한 파일은 낡는다. 그러면 AI가 낡은 관계를 진실로 읽는다. — *claude_code (draft)*
- **Graph 용도**: 결정의 근거 추적, 결정 전 영향 범위 확인, 존재 이유 설명, 빠진 것 찾기, 서로 부딪히는 결정 찾기, 깨진 가정에 기댄 결정 찾기, AI 설명의 사실 확인

### DEC-011 기간 단위 운영

- **결정**: 작업을 기간으로 나눈다.
  - **시작(계획)**: 작업별 위험 등급을 판정하고, high 작업의 승인자를 지정하고, 미결정 수(R4)를 확인한다.
  - **완료**: 기간 중 내린 high 결정을 다시 본다.
- **채택**: 사람 제안
- **이유**: 아래 세 가지를 함께 해결한다. — *claude_code (draft)*
  - 1인일 때 high 작업의 대체 통제 (시간 간격)
  - 다시 보기 계기 (R7)
  - 미결정 정리 시점
  - 팀으로 운영 할것이고 Weekly / Monthly/ Quarter/Half/Year 로 구분한다. — *Sun&Moon(생각)* (→ DEC-021)
- **미정**: 기간 길이 → DEC-021에서 기간 체계를 정했다. 계획과 완료를 어느 주기에 할지는 아직 정하지 않았다.

### DEC-012 결정 기록 요구사항

- **결정**: 아래 "합의된 규칙"의 R1~R6
- **AI 추천에서 바뀐 점**:
  - R1: 대안 2개 이상 → 추천 중심, 대안이 있으면 보여줌
  - R4: 상한 3개 → 5개
  - R5: 한 화면 이내 → 근거와 참고자료를 명시하고 요약
- **채택**: AI 추천 수정
- **이유**: 미결정이 3개면 고민하는 동안 다른 일을 할 수 없다. 근거와 참고자료가 있어야 다른 사람을 설득하고 설명할 수 있다. — *Sun&Moon (발언 요약)*

### DEC-013 저장소에 기록된 것만 결정으로 인정

- **결정**:
  - AI가 과거 결정을 언급할 때는 결정 ID를 함께 제시한다.
  - ID가 없으면 그것은 결정이 아니라 AI의 기억이다.
  - AI의 기억과 저장소 기록이 다르면 저장소 기록을 따른다.
- **채택**: AI 추천 그대로
- **이유**: Claude Code가 "전에 결정하셨어요"라고 하는데 그 근거를 찾지 못하는 일이 많다. — *Sun&Moon (발언 요약)*
- **결과**: FULL-CONTEXT §18의 열린 질문 "AI의 기억과 저장소의 공식 기록 중 무엇을 우선하는가"에 대한 답이다. 짧은 session을 여러 개 써도 기억이 사라지지 않는 근거이기도 하다. 기억은 대화가 아니라 저장소에 남는다.

### DEC-014 원본 경계

- **결정**: 작업 진행 상태의 원본은 Jira, 결정과 설계의 원본은 저장소다.
- **채택**: AI 추천 그대로
- **이유**: 같은 사실을 두 시스템에서 편집하지 않는다 (02 원칙). — *claude_code (draft)*
  - Jira는 작업 진행 상태 및 방향성, 저장소는 결정 및 설계 문서 그리고 소스 — *Sun&Moon(생각)*
  - 방향성은 설계하다 막힐 때 어떻게 가야 할지에 대한 흐름을 정리하는 것을 말한다. — *Sun&Moon (발언 요약)*

### DEC-015 설계 변경 시 결정 기록 필수

- **결정**: 아래 "합의된 규칙"의 설계 변경 규칙
- **채택**: 사람 제안 (예: 설계는 Oracle이었는데 비용 문제로 MS-SQL로 바꿈, 설계는 Java였는데 Go로 바꿈)
- **이유**: 개발 중에 비용이나 기술 한계 때문에 설계가 바뀌는 일은 반드시 관리되어야 한다. — *Sun&Moon (발언 요약)*
- **참고**: AI가 에러에 막혀 라이브러리나 구현 방식을 묻지 않고 바꾸는 경우도 여기에 해당한다.

### DEC-016 Verification 범위

- **결정**: Verification(확인 방법)으로 자동 검사(CI, 스크립트)와 체크리스트 항목(PR 체크 항목 등, 누가 봐도 지켰는지 판별 가능한 기준)을 모두 인정한다.
- **AI 추천**: 이 안
- **대안**: 자동 검사만 인정
- **채택**: AI 추천 그대로
- **이유**: 아직 CI가 없어서, 자동 검사만 인정하면 당분간 MUST 규칙이 거의 없어진다. — *claude_code (draft)*
  - CI에 대한 계획을 수립 해 보는 것은 어떤가? 지금 CI에 대한 계획을 수립 하는 것은 어려움이 있을까? 고민이 필요해 보인다. 자동 검사와 CI.. 그 차이가 무엇이 될까도 고민이 필요해 보인다. — *Sun&Moon(질문과 생각)*
  - 자동 검사는 무엇을 검사하는가(스크립트)이고, CI는 그 검사를 언제 자동으로 돌리는가(예: PR마다 GitHub Actions 실행)이다. CI 계획은 GitHub 연동과 결정 기록 포맷이 정해진 뒤에 세운다. — *claude_code (참고)*

### DEC-017 high 결정은 사람이 확인해야 진행

- **결정**:
  - high 위험 등급 결정은 사람이 이유를 직접 쓰거나 AI draft를 확인하기 전까지 진행하지 않는다.
  - 사람이 직접 쓰지 않아도 된다. 대신 최소한 "확인함" 코멘트를 남긴다. GitHub에서 저장소를 지울 때 확인 입력을 요구하는 것과 같은 방식이다.
- **AI 추천**: high는 사람이 이유를 직접 써야 함 (R2의 예외)
- **채택**: AI 추천 수정 (직접 작성 대신 명시적 확인으로 완화)
- **이유**: 모든 이유를 직접 쓰게 하면 결국 포기하게 된다. — *claude_code (draft)*
  - 확인했다는 흔적을 남기는 행위만으로도 그냥 넘기는 것을 막을 수 있다. 솔직히 지금은 많은 것을 협의하고 결정해야 할 시기이다. 어떤것도 claude_code 의견 대로 할수는 없을 것 같다. — *Sun&Moon(생각)*
- **보완 대상**: DEC-012의 R2

### DEC-018 규칙 문장은 영어가 원본

- **결정**: 규칙 문장은 영어가 원본이고, 한국어는 괄호 안의 참고 번역이다. 둘이 다르면 영어를 따른다. 긴 설명은 한국어로만 쓴다.
- **AI 추천**: 한국어가 원본
- **채택**: 사람 제안 (추천과 다름)
- **이유**: 영어에 익숙해지고 싶다. 번역기를 쓰고, 궁금한 것은 토큰을 써서라도 질문하겠다. — *Sun&Moon (발언 요약)*
- **replaces**: DEC-007의 언어 부분 ("한국어로 쓰고 괄호 안에 영어")

### DEC-019 확인되지 않은 draft는 미결정으로 셈

- **결정**: R4의 미결정에는 아직 선택하지 않은 결정과, 이유가 AI draft인데 아직 확인되지 않은 결정이 모두 들어간다. "확인함"이 기록되면 미결정에서 빠진다.
- **AI 추천**: draft는 세지 않음
- **채택**: AI 추천 수정
- **이유**: draft를 하나씩은 막지 않지만, 쌓이면 상한에 걸리게 해서 방치되지 않게 한다. — *claude_code (draft)*
  -  ai 추천 역시 한번은 코멘트를 해야 할 것 같다. ai 추천이 이해하지 못하면 추천이 아닌 결정이 되니까. — *Sun&Moon(생각)*
  - Claude Code의 draft도 하나의 답변이다. 사람이 확인해야 답변으로 완성된다. — *Sun&Moon (발언 요약)*
- **보완 대상**: DEC-012의 R4

### DEC-020 위험 등급은 영어로만 표시

- **결정**: `risk_level`은 `low`, `medium`, `high`로만 표시한다. 한국어 이름(경량, 표준, 고위험)은 쓰지 않는다.
- **채택**: 사람 제안
- **이유**:
- 규칙 문장을 영어 원본으로 정한 DEC-018과 표기를 맞춘다. — *claude_code (draft)*
- 영어로 한다. 결정함 — *Sun&Moon (결정)*
- **replaces**: DEC-008의 한국어 병기 (`low`(경량) 등)

### DEC-021 기간 체계

- **결정**: 기간을 Weekly / Monthly / Quarter / Half / Year로 구분한다.
- **채택**: 사람 제안
- **이유**: 팀으로 운영할 것이다. — *Sun&Moon(생각)* (DEC-011에 쓴 글)
- **미정**: 주기별로 할 일, DEC-011의 계획과 완료를 어느 주기에 할지 (미해결 참고)
- **보완 대상**: DEC-011

### DEC-022 GitHub 공개 저장소

- **결정**: 프레임워크를 GitHub 공개(public) 저장소로 관리한다.
  - 저장소 이름: `AI-Native-Development-Rules` (GitHub 저장소 이름에는 공백을 쓸 수 없다)
  - 설명: AI Native Development Rules
- **AI 추천**: 없음 (공개 범위를 Sun&Moon에게 물음)
- **채택**: 사람 제안
- **이유**: public으로 해도 재미있을 것 같다. — *Sun&Moon (발언 요약)*
- **영향**: 문서, 결정 기록, 커밋 이력이 모두 공개된다.

---

## 합의된 규칙

규칙 문장은 영어가 원본이다. 괄호 안의 한국어는 참고 번역이다 (DEC-018).

**Verification 범위** (DEC-016)
- Verification may be an automated check or a checklist item anyone can judge. (확인 방법은 자동 검사이거나, 누구나 판별할 수 있는 체크리스트 항목이다.)

**R1 추천과 대안**

- [MUST] The AI must present a recommendation with its reason. (AI는 추천과 추천 이유를 제시한다.)
- [SHOULD] Show alternatives if any exist. (다른 대안이 있으면 함께 보여준다.)
- Verification: The decision record has recommendation and reason fields. (결정 기록에 추천 필드와 이유 필드가 있다.)

**R2 선택 이유** (DEC-012, DEC-017)
- [SHOULD] The reason should be written by a human. (선택 이유는 사람이 쓴다.)
- [MUST] An AI-written reason must be marked as draft with its author name. (AI가 쓴 이유는 작성자 이름과 함께 draft로 표시한다.)
- A human confirms a draft with the comment `DEC-xxx 확인함`, and the confirmer and date are recorded. (사람은 `DEC-xxx 확인함` 코멘트로 draft를 확인하고, 확인자와 날짜를 기록한다.)
- [MUST] For high risk, do not proceed until a human writes or confirms the reason. (high 위험 등급은 사람이 이유를 쓰거나 확인하기 전까지 진행하지 않는다.)
- Verification: Every high decision has a human-written reason or a confirmation record. (모든 high 결정에 사람이 쓴 이유나 확인 기록이 있다.)

**R3 채택 방식 표시**
- [MUST] PRs and commits must show the decision ID and how it was adopted. (PR이나 커밋에 결정 ID와 채택 방식을 표시한다.)
- Verification: PR template item. (PR 템플릿 항목)

**R4 미결정 상한** (DEC-012, DEC-019)
- [MUST] When more than five decisions are pending, resolve them before adding a new one. (미결정이 5개를 넘으면 새 결정을 등록하기 전에 정리한다.)
- Pending means no option is selected, or the reason is an unconfirmed AI draft. (미결정은 아직 선택하지 않은 결정, 또는 이유가 확인되지 않은 AI draft인 결정이다.)
- Verification: Count pending decisions. (미결정 수를 센다.)

**R5 근거 명시**
- [MUST] A decision record must state the conclusion, reason, evidence summary, and references. (결정 기록에 결론, 이유, 근거 요약, 참고자료 출처를 명시한다.)
- Verification: Required fields in the decision record. (결정 기록의 필수 필드)

**R6 결정 역할**
- [MUST] Record the decision owner role. (결정한 역할을 기록한다.)
- Verification: Required field in the decision record. (결정 기록의 필수 필드)

**설계 변경** (DEC-015)
- [MUST] Record a decision before changing any technology or structure defined in current_state. This applies to AI agents too. (설계와 다른 기술이나 구조로 바꾸려면 구현 전에 결정 기록을 만든다. AI Agent도 같다.)
- Verification: A PR that changes dependencies, DB config, or language without a decision ID is rejected. (결정 ID 없이 의존성, DB 설정, 언어를 변경한 PR은 반려한다.)

**결정 ID 제시** (DEC-013)
- [MUST] When citing a past decision, the AI must provide its decision ID. (AI가 과거 결정을 근거로 말할 때는 결정 ID를 함께 제시한다.)
- Verification: If the AI says "previously decided" without an ID, the user asks for the ID. (AI가 ID 없이 "이전에 결정했다"고 하면 사용자가 ID를 요구한다.)

**위험 등급별 규칙** (DEC-008, DEC-017)

| Rule | low | medium | high |
|---|---|---|---|
| Decision record (결정 기록) | not required | SHOULD | MUST |
| Reason written or confirmed by a human (사람이 쓰거나 확인한 이유) | — | SHOULD (미확인 draft는 R4에 셈) | MUST (확인 전 진행 불가) |
| Approval by a role other than the author (작성자가 아닌 역할의 승인) | — | — | MUST |

---

## 미확인 draft (R4 집계)

**미결정: 0개 / 상한 5개.** Sun&Moon이 직접 글을 남긴 결정은 확인된 것으로 본다 (표기의 확인 판정).

| ID | 결정 | AI가 쓴 이유 (draft) |
|---|---|---|


## 미해결

- **다음 작업: 결정 기록 포맷 설계** (Human View와 Agent View). 2026-10-20 정리 과정에서 드러난 필요한 칸:
  - 이유를 작성자별로 나눠 적는 칸
  - 결정과 이유를 분리하는 칸 (이유 칸에 새 결정이 섞여 들어갔음)
  - 질문을 남기는 칸
- 결정 기록에서 남은 단계:
  - 산출물 중 어디에 선택이 있는지 찾기
  - 다시 보기 계기 (R7). 후보는 기간을 마칠 때 다시 보기(DEC-011)와 깨진 가정 추적(DEC-010)이다.
- DEC-021의 주기별 할 일과, DEC-011의 계획과 완료를 어느 주기에 할지. claude_code 추천은 다음과 같다.
  - Weekly: 작업 계획과 완료, high 결정 다시 보기
  - Monthly: PM/PL용 Graph 보고서, 미확인 draft 정리
  - Quarter: 우선순위와 opportunity 다시 보기
  - Half / Year: vision 다시 보기, 운영 결과를 00으로 환류
- 위험 등급을 매기는 위치 (DEC-008의 질문). claude_code 추천: 작업은 Jira 이슈 필드에, 결정은 결정 기록의 `risk_level`에 둔다.
- CI 계획 (DEC-016): GitHub 연동과 결정 기록 포맷이 정해진 뒤에 세운다.
- once와 always 권한 선택 방식 (DEC-009): Claude Code 부록(A1)에 넣을 후보다.
- A 항목:
  - A1 적용 가이드와 Claude Code 부록
  - **A2 00 산출물 명세**
  - A4 01의 단계별 산출물
  - A5 산출물 생성 시점 표
- v03에 반영할 때 함께 고칠 것:
  - 결정 포맷 3종 통일 (01 §4, 02 §9, 08 §7)
  - 02 §9 예시에 이유 필드가 없음
  - Vision Decision Owner가 00 §9에서는 미해결인데 01 §6과 08 §7에서는 정해져 있음
  - 00 흐름에서 `assumptions`와 `evidence`의 순서 확인
- 그룹 3 (팀 결정권): 역할 사이의 결정 충돌 해결, 위험 등급 하향 승인, Orchestrator 권한, 최소 Gate
- 그룹 4 (실제 프로젝트에 적용한 뒤 결정): Context Budget, 요약 손실 평가, Context Manifest 자동 생성, MCP 보안 경계, 관계 스키마 세부, CI 실패 수준, Multi-Agent 전환 시점, Graph DB 도입 시점, 질문 피로 측정, Evidence 신뢰 등급, 이중 View 유지 비용
- 00.common 을 idea_space, problem_space, assumptions, evidence, opportunity, vision, decision에 공통으로 적용되는 표현, 식별, 연결, 보고 및 검토의 기반 규칙을 정의한다.
  - 00.common
    → 전체 영역을 연결하는 공통 계약으로 정의하고 정리 한다.
  - 각 영역
    → 자신만의 의미, 상태, 필드와 생명주기
  - 00.common 에는 Review 와 Report 를 관리 하도록 한다. 이것에 대해서 넣어야 할 공간이 명확하지 않아서 생긴 고민
