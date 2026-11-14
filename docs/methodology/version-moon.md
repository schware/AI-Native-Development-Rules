# Version Moon

- 확정: 2026-11-14, Sun&Moon
- 공통 원칙과 공통 장치(작업 요청 형식, PR Report, 결정 기록 쓰는 법, Five-line Check, 막는 장치)는 [`README.md`](README.md)에 있다.
- 용어의 뜻은 맨 아래 [용어 설명](#10-용어-설명)에 있다.

## 한눈에
- 처음에 Charter 하나로 Product Goal과 끝(MVP)을 정한다.
- 그 뒤로는 Issue를 하나씩 만들고 Retrospective로 돌아보며 나아간다. 열린 Issue는 늘 하나다.
- Add-on은 처음부터 두지 않는다. DoR 점검과, 진행 중에 생긴 일로 켠다.

## 왜 이렇게 하는가
사람 팀에는 기억하고, 되묻고, 반대하고, 만드는 데 시간이 드는 자연스러운 안전장치가 있다. AI Agent에는 이것이 없다. 그래서 빈칸을 추측으로 채우고 "가능합니다", "완료했습니다"라고 말한다. Version Moon은 이 안전장치를 체크리스트로 다시 세운 Agile이다. 막힐 것을 미리 가정하지 않고, 일이 생겼을 때만 Add-on을 켠다.

---

## 흐름

```text
Charter → [ DoR → 진행 → DoD → Retrospective ] 반복 → 끝 (Done 또는 Archive)
```

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
| **Issue** | 일 하나. 열린 Issue는 늘 하나 | 일반 Agile의 User Story에 해당 |
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
