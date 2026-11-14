# Version Moon

- 확정: 2026-11-14, Sun&Moon
- 공통 원칙과 공통 장치(작업 요청 형식, PR Report, 결정 기록 쓰는 법, Five-line Check, 막는 장치)는 [`README.md`](README.md)에 있다.
- 용어의 뜻은 맨 아래 [용어 설명](#10-용어-설명)에 있다.

## 한눈에
- 처음에 Charter 하나로 Product Goal과 끝(MVP)을 정한다.
- 그 뒤로는 Issue를 하나씩 만들고 Retrospective로 돌아보며 나아간다. 열린 Issue는 늘 하나다(Epic Issue는 세지 않는다).
- Add-on은 처음부터 두지 않는다. DoR 점검과, 진행 중에 생긴 일로 켠다.

## 왜 이렇게 하는가
사람 팀에는 기억하고, 되묻고, 반대하고, 만드는 데 시간이 드는 자연스러운 안전장치가 있다. AI Agent에는 이것이 없다. 그래서 빈칸을 추측으로 채우고 "가능합니다", "완료했습니다"라고 말한다. Version Moon은 이 안전장치를 체크리스트로 다시 세운 Agile이다. 막힐 것을 미리 가정하지 않고, 일이 생겼을 때만 Add-on을 켠다.

---

## 흐름

```text
Charter → [ DoR → 진행 → DoD → Retrospective ] 반복 → 끝 (Done 또는 Archive)
```

## 구조: Epic, Release, Issue

Issue는 Epic을 대신하지 않는다. **Epic은 Release 하나이고, Release 안에 Issue가 여러 개 있다.** 기능을 만드는 Issue가 일반 Agile의 User Story에 해당한다.

```text
Product Goal (Charter, 한 문장)
└─ Epic List (Charter, 결정된 방향)
   ├─ Epic 1 = Release 1 (끝 = MVP)          → Epic Issue #10
   │  ├─ User Story: Walking Skeleton        → Sub-issue #11
   │  ├─ User Story                           → Sub-issue #12
   │  ├─ Spike                                → Sub-issue #13
   │  └─ User Story                           → Sub-issue #14  (닫히면 Epic 1 완료)
   ├─ Epic 2 = Release 2                     → Epic Issue #20
   └─ Epic 3 = Release 3
```

| 단위 | 크기 | 어디에 적나 | 누가 정하나 |
|---|---|---|---|
| **Product Goal** | 프로젝트 전체 | Charter | 사람 |
| **Epic** (= Release) | 쓸 수 있는 상태 하나. Issue 여러 개 | Charter의 Epic List(이름과 최소 목표 한 줄), GitHub의 Epic Issue | 사람 (Learning에서 결정) |
| **Issue** | Estimate 안에 끝나는 일 하나 | GitHub Issue (Epic Issue의 Sub-issue) | Release Planning에서 사람이 고른다. AI는 나누는 안을 낸다 |

## Issue의 종류와 등록 방법

### 종류
| 종류 | label | 쓰는 때 | 형식 |
|---|---|---|---|
| **Epic Issue** | `epic` | Release 하나를 묶는다 | 이름, 최소 목표(Epic List의 한 줄), Release Goal, Acceptance Criteria |
| **User Story** | — | 기능을 만든다 | 누가 / 무엇을 / 왜. 예: "개발자는 브라우저로 workspace에 들어가서, 노트북 설정 없이 개발을 시작한다" |
| **Spike** | `spike` | 모르는 것을 확인한다 | 확인할 질문, 끝나는 기준, timebox |
| **Bug** | `bug` | 만든 것이 Acceptance Criteria대로 동작하지 않는다 | 기대한 동작, 실제 동작, 다시 만드는 방법 |
| **Decision Candidate** | `decision-needed` | 사람의 결정이 필요하다 | 결정 기록 초안(`proposed`) 링크 |

막힌 Issue에는 종류와 상관없이 `blocked` label을 더한다.

### 등록 순서
1. Release Planning에서 **Epic Issue**를 하나 연다.
2. 이번 Release에서 할 Issue를 Epic Issue의 **Sub-issues**로 단다. `gh`로 연결할 수 없으면 웹에서 연결하거나, Epic Issue 본문에 자식 Issue 번호를 체크리스트로 적는다.
3. 열린 Issue를 셀 때 **Epic Issue는 세지 않는다.** 열린 Issue 하나는 User Story, Spike, Bug, Decision Candidate 중에서 센다.
4. Sub-issues가 모두 닫히고 Release의 Retrospective를 마치면 Epic Issue를 닫는다.

### 크기를 맞추는 규칙
- Issue가 Estimate 안에 끝나지 않을 것 같으면 나눈다. 나눌 수 없으면 Spike로 먼저 확인한다.
- Epic의 Issue가 Backlog 상한(5개)을 넘으면 Epic이 너무 크다는 뜻이다. Release를 나누고, 나눈 결과는 결정 기록으로 남겨 Epic List를 고친다.
- Issue는 한 Epic에만 속한다. 다른 Epic의 일이 필요해지면, 지금 Release Goal에 꼭 필요한지 본다. 필요하지 않으면 그 Epic의 Release Planning 때 다룬다.

## Release와 branch

### Release
- Epic이 끝나면 main에 **tag**를 붙이고 **GitHub Release**를 만든다. 예: Epic 1(MVP) 완료 → `v0.1.0`, Epic 2 완료 → `v0.2.0`.
- release note에는 닫힌 Issue 목록과 Retrospective 링크를 둔다.
- Release는 branch가 아니라 main 위의 tag다. tag는 "이 시점에 이 Epic이 끝났다"는 책갈피다.

### branch (GitHub Flow)

```text
main ─●──●──●──●──●──────●──●──●──●──●──→
      #11 #12 #13 #14 #15  #21 #22 #23 #24 #25
                       ↑                    ↑
                  tag v0.1.0           tag v0.2.0
```

- branch는 **Issue 하나에 하나**. main에서 따고, PR로 main에 돌아오고, merge 뒤 지운다. 다음 Issue는 다시 main에서 딴다.
- **Epic branch와 Release branch는 만들지 않는다.** Epic branch에 쌓아 두다가 한 번에 합치면, 떨어져 있던 만큼 충돌이 커진다.
- **Spike branch는 merge하지 않는다.** 결과는 결정 기록으로 남기고 지운다.
- **merge된 main은 언제나 동작해야 한다.** User Story는 그 자체로 동작하고 test를 통과해야 merge한다. 아직 쓰면 안 되는 기능은 화면에 연결하지 않은 채로 둔다.

### 이미 낸 버전을 급히 고칠 때 (hotfix)
main에는 이미 다음 Epic이 반쯤 들어 있을 수 있다. 그래서 이때만 예외로 tag에서 branch를 딴다.

```text
main ─●──●──●──●──●──────●──●──●───────●──→
                       ↑         \         ↑
                    v0.1.0        \     main에도 같은 수정을 넣는다
                       \           \
                        └─ hotfix ─●── tag v0.1.1
```

1. tag `v0.1.0`에서 hotfix branch를 딴다.
2. 고치고 tag `v0.1.1`을 붙인다.
3. 같은 수정을 main에도 넣는다. 안 넣으면 다음 Release에서 같은 Bug가 다시 나온다.

## 1. Charter (`docs/plan-baseline.md`)
프로젝트에 하나만 둔다. 모두 채워야 시작한다.
- [ ] **Product Goal**: 누구를 위해, 무엇을 만들어, 어떤 문제를 푸는가
- [ ] **Out of Scope**: 하지 않는 것
- [ ] **MVP**: 첫 번째 Release가 끝났을 때 쓸 수 있는 상태. 한두 문장
- [ ] **Epic List**: Release 후보(Epic)의 이름과 최소 목표 한 줄씩. Learning에서 그린 큰 그림 한 장을 결정한 것이다. 자세한 내용(Story, 일정)은 Learning 공간에 두고 저장소에는 두지 않는다
- [ ] **Stop Condition**: 이것이 드러나면 멈춘다. 없으면 "없음"
- [ ] AI가 낸 더 작은 안, 더 큰 안, Pre-mortem("실패한다면 이유는?")을 보고 사람이 정했다
- [ ] 결정 기록으로 남기고, AI가 고칠 수 없도록 잠갔다
- [ ] **Walking Skeleton**: 첫 Issue. 처음부터 끝까지 한 번 이어지는 가장 작은 기능

Charter는 고정한다. Product Goal이나 Out of Scope를 바꿔야 할 때만 결정 기록을 남기고 고친다.

Epic List도 Charter와 함께 고정한다. Epic List는 결정된 방향이고, 바뀌는 것은 다음에 어느 Epic부터 할지다. 방향이 바뀔 때만 결정 기록을 남기고 Epic List를 고친다.

전혀 다른 제품을 만들고 싶으면 이 프로젝트를 끝내고 새 프로젝트를 시작한다.

## 2. DoR (Issue 시작 점검)
**꼭 쓸 것**
- [ ] Acceptance Criteria
- [ ] Estimate

**사람이 답할 질문** (그렇다면 해당 Add-on을 켠다)
- [ ] 밖에서 기다려야 하는 것이 있는가 → **Blocker**
- [ ] 모르거나 아직 정하지 않은 것이 있는가 → **Spike, Decision Candidate**
- [ ] 사람에게 보내거나, 밖으로 나가거나, 데이터를 지우거나 바꾸는가 → **Assumption List**
- [ ] 기다리는 Issue가 둘 이상인가 → **Release Planning, Backlog**

## 3. 진행 중 Watch (AI가 센다)
하나라도 해당하면 AI는 알리고 멈춘다.
- [ ] Estimate의 두 배를 넘었다 → **Risk**
- [ ] 같은 오류를 세 번 넘게 고치려 했다 → **Risk**
- [ ] Charter의 Stop Condition에 해당한다 → **Risk**. 멈추고 사람이 결정한다
- [ ] Assumption List에 없는 가정이 새로 필요하다 → **Assumption List에 더한다**
- [ ] Blocker가 3개가 되었다 → **진행을 멈춘다** (Stop Rule)
- [ ] Retrospective 생략이 3번 이어졌다 → **진행을 멈춘다** (Stop Rule)

## 4. DoD (Issue 마무리)
**PR Report**: [`README.md`](README.md) 3.2를 따른다.

**Retrospective (`docs/journey.md`, 사람이 먼저 쓴다)**
- [ ] 잘 안 된 것. 없으면 "없음", 쓰지 못했으면 "생략". 둘은 다르다
- [ ] 알게 된 것

## 5. 새 session을 시작할 때
- session은 Retrospective를 마친 뒤에만 바꾼다.
- 새 session은 [`README.md`](README.md) 3.4의 Five-line Check를 한다. 셋째 줄에는 켜져 있는 Add-on(Blocker, Risk, Backlog)을 적는다.

## 6. 끝
- [ ] **Done**: MVP에 닿았다. 더 갈지는 Release Planning에서 정한다
- [ ] **Archive**: 더 진행하지 않는다. 배운 것을 마지막 Retrospective에 남긴다

---

## 7. Add-on (필요할 때 켠다)
- AI는 켜야 할 때를 보면, **어떤 Add-on을 왜 켜야 하는지 말하고 멈춘다.** 켤지는 사람이 정한다.
- 할 일이 끝나면 끈다.

| Add-on | 하는 일 | 끄는 때 |
|---|---|---|
| **Blocker** | Issue에 `blocked` label을 붙이고, 무엇을, 누구를, 언제까지 기다리는지 적는다. 그동안 다른 Issue를 먼저 한다. **3개가 되면 Claude Code는 진행을 멈추고** Release Planning을 연다 | 풀리면 label을 떼고 이어서 한다 |
| **Spike** | 확인할 질문, 끝나는 기준, timebox를 정한 Issue 하나로 만든다. 따로 branch에서 하고 merge하지 않는다. 결과는 결정 기록으로 남긴다 | timebox가 지나거나 답이 나오면 닫는다 |
| **Decision Candidate** | AI가 결정 후보(`proposed`)를 쓴다. 찾아본 기존 결정과 바꾸는 것을 함께 적는다. Issue에 `decision-needed` label을 붙인다. 결정 전에는 그 부분을 시작하지 않는다 | 사람이 결정하면 끝난다 |
| **Assumption List** | AI가 5W2H 표를 만들고, 칸마다 "요청", "가정", "빈칸"으로 표시한다. 사람은 "가정"만 보고 "빈칸"은 반드시 채운다. 확인한 표에서 Scenario와 test를 만든다 | 표를 확인하면 끝난다. 새 가정이 생기면 다시 켠다 |
| **Release Planning** | Decision Candidate와 Blocker부터 본다. Charter의 Epic List에서 다음 Release를 고르고, 고른 결과는 `docs/plan.md`에 적는다. Release Goal과 Acceptance Criteria를 정하고, 이번에 할 Issue를 고른다. Pre-mortem("이번 Release가 실패한다면 이유는?")을 한다 | Release가 끝나면 끝난다 |
| **Backlog** (`docs/backlog.md`) | Release Planning 때만 채운다. 이번 Release에서 할 Issue만, 최대 5개. 넘으면 Release를 나눈다. Release 중에는 Release Goal에 꼭 필요한 것만 더한다. 넣고 순서를 정하는 것은 사람이 한다 | 비면 끈다. Release가 끝날 때 남은 것은 넘길지 버릴지 정한다 |
| **Risk Register** (`docs/risks.md`) | Risk의 신호를 셀 수 있는 사실로 적고 대응을 정한다. Stop Condition에 해당하면 멈추고, 계속, 목표 변경, Archive 중 하나를 결정 기록으로 남긴다 | 신호가 사라지거나 결정이 나면 "닫힘" |

---

## 8. 문서
Charter는 고정하고, 나머지는 쌓아 간다. 지난 내용은 지우거나 고치지 않는다.

| 문서 | 언제 생기나 | 어떻게 늘어나나 |
|---|---|---|
| `docs/plan-baseline.md` | 시작할 때 | 고정 (Charter, Epic List) |
| `docs/plan.md` | 시작할 때 | Release마다 절이 추가된다. 맨 위 "Version Moon / 현재 Release / 현재 Issue"만 바뀐다 |
| `docs/journey.md` | 시작할 때 | Issue와 Release마다 Retrospective가 추가된다 |
| `records/07.decision/` | 시작할 때 | 결정마다 파일이 추가된다. 이전 결정은 고치지 않는다 |
| `docs/backlog.md` | Backlog를 켤 때 | Release마다 채우고 비운다 |
| `docs/risks.md` | Risk Register를 켤 때 | Risk가 추가되고 닫힌다 |

## 9. Stop Rule

| 기준 | 수 | 그다음 |
|---|---|---|
| Blocker | 3개 | Claude Code는 진행을 멈춘다. Release Planning을 열어 기다릴지, 목표를 바꿀지, Archive할지 정한다 |
| Retrospective 생략 | 3번 연속 | Claude Code는 진행을 멈춘다. 밀린 Retrospective를 쓰거나, 생략한 이유를 적고 다시 시작한다 |

---

## 10. 용어 설명
이 방법론에서의 뜻이다. 일반 Agile과 다른 곳은 "일반 Agile과 다른 점"에 적었다.

| 용어 | 뜻 | 일반 Agile과 다른 점 |
|---|---|---|
| **Charter** (헌장) | 프로젝트에 하나 두는 고정 문서. Product Goal, Out of Scope, MVP, Epic List, Stop Condition을 담는다 | 일반 Agile의 Product Vision 역할 |
| **Product Goal** (제품 목표) | 누구를 위해, 무엇을 만들어, 어떤 문제를 푸는가. 한 문장 | |
| **Out of Scope** (하지 않는 것) | 이 프로젝트에서 만들지 않는 것 | |
| **MVP** (최소 제품) | 첫 번째 Release가 끝났을 때 쓸 수 있는 상태 | 기능 목록이 아니라 상태로 쓴다 |
| **Epic** (큰 덩어리) | 큰 그림의 한 칸 | 여기서는 Epic 하나 = Release 하나. 일반 Agile에서는 여러 Release에 걸치기도 한다 |
| **Epic List** (큰 그림) | Learning에서 결정한 Epic의 이름과 최소 목표 목록. 결정된 방향 | Roadmap이라 부르지 않는다. 일반적으로 Roadmap은 계속 바뀌는 것으로 통하기 때문이다 |
| **Release** (릴리스) | Epic 하나를 만드는 단위. 첫 Release의 끝이 MVP | |
| **Release Planning** (릴리스 계획) | Epic List에서 다음 Release를 고르고, 이번에 할 Issue를 정하는 시기 | 정해진 주기 없이, 필요할 때 연다 |
| **Release Goal** (릴리스 목표) | 이번 Release가 끝났을 때의 상태 | |
| **Backlog** (백로그) | 이번 Release에서 꺼낼 Issue 목록. 최대 5개 | 일반 Agile의 Product Backlog처럼 쌓아 두지 않는다. 들어가는 곳이 아니라 나오기 위한 목록 |
| **Issue** | Estimate 안에 끝나는 일 하나. Release 안에 여러 개 있고, 열린 Issue는 늘 하나(Epic Issue 제외). 종류는 User Story, Spike, Bug, Decision Candidate | Epic을 대신하지 않는다 |
| **Epic Issue** | Release 하나를 묶는 GitHub Issue. `epic` label. Sub-issues가 모두 닫히고 Retrospective를 마치면 닫는다 | WIP에 세지 않는다 |
| **Sub-issues** (하위 Issue) | GitHub에서 Issue 아래에 자식 Issue를 다는 기능. Epic Issue에 진행률이 보인다 | Milestone은 역할이 겹쳐 쓰지 않는다 |
| **User Story** | 기능을 만드는 Issue. 누가 / 무엇을 / 왜로 쓴다 | 일반 Agile과 같다 |
| **Bug** | Acceptance Criteria대로 동작하지 않는 것을 고치는 Issue | |
| **tag** | main의 한 시점에 붙이는 이름. Epic이 끝난 자리의 책갈피 | |
| **GitHub Release** | tag에 release note를 붙여 "이 버전을 냈다"를 남기는 기능 | Release(릴리스)는 일의 단위이고, GitHub Release는 그 끝을 기록하는 기능이다 |
| **hotfix** | 이미 낸 버전을 급히 고치는 것. tag에서 branch를 따고, 같은 수정을 main에도 넣는다 | 유일하게 main이 아닌 곳에서 branch를 딴다 |
| **Walking Skeleton** (첫 Issue) | 처음부터 끝까지 한 번 이어지는 가장 작은 기능 | |
| **DoR** (Definition of Ready, 시작 점검) | Issue를 시작하기 전에 갖출 것 | |
| **Acceptance Criteria** (끝났다는 기준) | Issue나 Release가 끝났다고 판단하는 기준 | |
| **Estimate** (예상 기간) | Issue에 걸릴 것으로 보는 기간 | 마감이 아니다. 두 배를 넘으면 Risk 신호. Story Point는 쓰지 않는다 |
| **DoD** (Definition of Done, 완료 정의) | Issue를 마무리할 때 갖출 것. PR Report와 Retrospective | |
| **PR Report** (PR 보고) | AI가 쓰고 사람이 검토하는 PR 보고. [`README.md`](README.md) 3.2 | |
| **Retrospective** (회고) | Issue와 Release가 끝날 때 돌아보는 기록. 사람이 먼저 쓴다 | 회의가 아니라 `docs/journey.md`의 짧은 기록 |
| **Sprint** | 쓰지 않는다 | 정해진 주기가 없다. Issue 하나씩 간다 |
| **Add-on** (필요할 때 켜는 장치) | 처음부터 두지 않고, 일이 생겼을 때 켜는 장치 | |
| **Blocker** (막힌 일) | 밖의 무언가를 기다려야 해서 진행할 수 없는 Issue | 모르는 것, 하기 싫은 것은 Blocker가 아니다 |
| **Spike** (확인 작업) | 모르는 것을 확인하는 Issue. timebox를 두고, merge하지 않는다 | PoC와 같은 뜻 |
| **Decision Candidate** (결정 후보) | AI가 쓰고 사람이 결정하는 결정 기록 초안(`proposed`) | |
| **Assumption List** (가정 목록) | AI가 요청의 빈칸을 5W2H로 드러낸 표. "요청", "가정", "빈칸"으로 나눈다 | |
| **Scenario** (시나리오) | 사람이 읽을 수 있게 쓴 확인할 상황. Scenario마다 test를 만든다 | 일반적으로 Acceptance Test라고도 한다 |
| **Risk** (위험) | 개발 중에 판단되는 이슈 가운데 그대로 두면 프로젝트를 멈추게 할 수 있는 것 | 일어날 수 있는 모든 일이 아니라, 멈출 사유가 되는 것만 |
| **Risk Register** (위험 목록) | Risk와 그 신호, 대응, 상태를 적는 문서 | |
| **Stop Condition** (멈출 조건) | Charter에 미리 적는, 드러나면 멈출 사유 | |
| **Stop Rule** (멈춤 기준) | Blocker 3개, Retrospective 생략 3번 연속이면 Claude Code가 진행을 멈춘다 | Lean의 Stop-the-line과 같은 생각 |
| **Pre-mortem** (사전 부검) | "실패한다면 이유는?"을 먼저 묻는 방법 | |
| **Five-line Check** (다섯 줄 확인) | 새 session이 작업 전에 현재 상태를 다섯 줄로 말하는 것. [`README.md`](README.md) 3.4 | |
| **Done / Archive** (완료 / 보관) | 프로젝트의 끝. Archive는 배운 것을 남기고 멈추는 것 | |
