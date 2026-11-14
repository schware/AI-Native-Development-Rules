# Version Moon

- 확정: 2026-11-14, Sun&Moon
- 공통 원칙과 공통 장치(작업 요청 형식, PR Report, 결정 기록 쓰는 법, Five-line Check, 막는 장치)는 [`README.md`](README.md)에 있습니다.
- 용어의 뜻은 맨 아래 [14. 용어 설명](#14-용어-설명)에 있습니다.

## 1. 한눈에

- 처음에 Charter 하나로 Product Goal, MVP, Epic List를 정합니다.
- 그 뒤로는 Issue를 하나씩 진행하고, 끝날 때마다 Retrospective를 씁니다. 한 번에 진행하는 Issue는 하나입니다.
- 문제를 다루는 역할은 셋으로 나뉩니다. Watch가 문제를 찾아 알리고, 사람이 무엇을 할지 정하고, Add-on으로 처리합니다.

### 왜 이렇게 하는가
개발 팀에서는 팀원 서로 기억하고, 되묻고, 반대하고, 만드는 데 시간이 들면서 자연스럽게 실수가 걸러집니다. AI Agent와의 작업은 이런 장치가 없어서 빈칸을 추측으로 채우고 "가능합니다", "완료했습니다"라고 답하는 과정의 연속이 됩니다. Version Moon은 이 장치를 체크리스트로 다시 세운 Agile 방법론을 적용해 보려고 합니다. 다만 막힐 것을 미리 가정하지 않고, 문제가 생겼을 때만 Add-on을 켭니다.

---

## 2. 흐름과 구조

```text
Charter
└─ Epic List (결정된 방향)
   ├─ Epic 1 = Release 1 (끝 = MVP)        → Epic Issue
   │   └─ [ DoR → 진행 → DoD → Retrospective ] × Issue 여러 개 → tag v0.1.0
   ├─ Epic 2 = Release 2                   → Epic Issue
   │   └─ [ … ] → tag v0.2.0
   └─ …
→ 끝 (Done 또는 Archive)
```

Epic 하나가 Release 하나이고, Release 안에는 Issue가 여러 개 있습니다. Issue가 Epic을 대신하지는 않습니다. 기능을 만드는 Issue는 일반 Agile의 User Story와 같습니다.

| 단위 | 크기 | 적는 곳 | 정하는 사람 |
|---|---|---|---|
| Product Goal | 프로젝트 전체 | Charter | 사람 |
| Epic (= Release) | 쓸 수 있는 상태 하나. Issue 여러 개 | Charter의 Epic List, GitHub의 Epic Issue | 사람 (Learning에서 결정) |
| Issue | Estimate 안에 끝나는 일 하나 | GitHub Issue (Epic Issue의 Sub-issue) | 사람이 Release Planning에서 고릅니다. AI는 나누는 안을 냅니다 |

---

## 3. Charter (`docs/plan-baseline.md`)

프로젝트에 하나만 둡니다. 아래를 모두 채운 뒤에 시작합니다.
- [ ] **Product Goal**: 누구를 위해, 무엇을 만들어, 어떤 문제를 푸는가
- [ ] **Out of Scope**: 이 프로젝트에서 하지 않는 것
- [ ] **MVP**: 첫 Release가 끝났을 때 쓸 수 있는 상태. 한두 문장
- [ ] **Epic List**: Epic의 이름과 최소 목표를 한 줄씩. Learning에서 그린 큰 그림 한 장을 결정한 것입니다. 자세한 내용(Story, 일정)은 Learning 공간에 두고 저장소에는 두지 않습니다
- [ ] **Stop Condition**: 드러나면 멈출 사유. 없으면 "없음"
- [ ] AI가 낸 더 작은 안, 더 큰 안, Pre-mortem을 보고 사람이 정했다
- [ ] 결정 기록으로 남기고, AI가 고칠 수 없도록 잠갔다
- [ ] Epic 1의 Epic Issue와 첫 Issue를 열었다. 첫 Issue는 Walking Skeleton이고, 되는지 확실하지 않으면 그것을 확인할 Spike다. Spike로 확인한 뒤 그 결과로 Walking Skeleton Issue를 만든다

### 고치는 경우
Charter는 고정합니다. 다음 경우에만 결정 기록을 남기고 고칩니다.
- Product Goal이나 Out of Scope가 바뀔 때
- Epic List의 방향이 바뀔 때: Epic을 더하거나 빼거나, 최소 목표가 바뀌는 경우
- Epic을 나눌 때(4.4): 목표는 그대로 두고 Epic만 둘로 나눕니다. 예를 들어 "Epic 2: 주문"을 "Epic 2a: 주문 접수"와 "Epic 2b: 주문 취소"로 나눕니다. 결정 기록에는 무엇을 무엇으로, 왜 나눴는지만 짧게 적습니다

다음에 어느 Epic부터 할지는 Charter를 고칠 일이 아닙니다. Release Planning에서 정하고 `docs/plan.md`에 적습니다.

진행하지 않기로 한 Epic은 지우지 않고, 그 줄에 "하지 않음"과 결정 기록 링크를 붙여 둡니다.

전혀 다른 제품을 만들고 싶어지면, 이 프로젝트를 끝내고 새 프로젝트로 시작합니다.

---

## 4. Issue

### 4.1 종류
| 종류 | label | 쓰는 때 | 적는 것 |
|---|---|---|---|
| Epic Issue | `epic` | Release 하나를 묶을 때 | 이름, 최소 목표(Epic List의 한 줄), Release Goal, Acceptance Criteria |
| User Story | — | 기능을 만들 때 | 누가, 무엇을, 왜. 예: "개발자는 브라우저로 workspace에 들어가서, 노트북 설정 없이 개발을 시작한다" |
| Spike | `spike` | 모르는 것을 확인할 때 | 11절 참고 |
| Bug | `bug` | 만든 것이 Acceptance Criteria대로 동작하지 않을 때 | 기대한 동작, 실제 동작, 다시 일으키는 방법 |
| Decision Candidate | `decision-needed` | 사람의 결정이 필요할 때 | 11절 참고 |

막힌 Issue에는 종류와 상관없이 `blocked` label을 더합니다.

### 4.2 등록
1. Epic Issue를 엽니다. 첫 Epic은 Charter를 잠글 때(3절), 그다음부터는 Release Planning에서 엽니다.
2. 이번 Release에서 할 Issue를 Epic Issue의 Sub-issues로 연결합니다. `gh`로 연결이 안 되면 웹에서 연결하거나, Epic Issue 본문에 자식 Issue 번호를 체크리스트로 적습니다.
3. Sub-issues가 모두 닫히고 Release의 Retrospective를 마치면 Epic Issue를 닫습니다.

### 4.3 진행 중인 Issue 세기
- 한 번에 진행하는 Issue는 하나입니다.
- Epic Issue와 `blocked` Issue는 세지 않습니다. 나머지(User Story, Spike, Bug, Decision Candidate) 중에서 하나만 진행합니다.
- Decision Candidate는 진행 중인 Issue로 셉니다. 결정이 나기 전에는 다음 일로 넘어가지 않기 위해서입니다.

### 4.4 크기
- Issue가 Estimate 안에 끝나지 않을 것 같으면 나눕니다. 나누기 어려우면 Spike로 먼저 확인합니다.
- Epic 하나에 들어가는 User Story와 Spike는 합쳐서 5개 이하로 합니다. Bug와 Decision Candidate는 세지 않습니다. 5개를 넘으면 Epic을 나눕니다(3절).
- 5개는 범위의 크기를 재는 기준입니다. Bug가 쌓이는 것은 크기가 아니라 품질의 문제여서, Watch에서 따로 봅니다(6절).
- Issue는 한 Epic에만 속합니다. 다른 Epic의 일이 필요해지면 지금 Release Goal에 꼭 필요한지 봅니다. 꼭 필요하지 않으면 그 Epic의 Release Planning 때 다룹니다.

---

## 5. DoR (Issue 시작 점검)

꼭 적을 것
- [ ] Acceptance Criteria
- [ ] Estimate. Spike는 Estimate 대신 timebox를 적습니다. Decision Candidate는 사람이 결정할 날짜를 적습니다

사람이 답할 질문 (해당하면 그 Add-on을 켭니다)
- [ ] 밖에서 기다려야 하는 것이 있는가 → Blocker
- [ ] 모르거나 아직 정하지 않은 것이 있는가 → Spike, Decision Candidate
- [ ] 사람에게 보내거나, 밖으로 나가거나, 데이터를 지우거나 바꾸는가 → Assumption List
- [ ] 기다리는 Issue가 둘 이상인가 → Release Planning, Backlog

## 6. Watch (진행 중 확인)

Watch는 **문제를 찾아 알리는 역할만** 합니다. 고치거나 판단하지는 않습니다. AI가 아래 신호를 찾으면 알리고 멈추며, 무엇을 할지는 사람이 정합니다.
- [ ] Estimate의 두 배를 넘었다 → Risk
- [ ] Spike의 timebox가 지났다 → 알린다. 닫는 것은 Spike의 규칙(11절)을 따른다
- [ ] Decision Candidate가 결정할 날짜를 넘겼다 → 사람에게 다시 알린다
- [ ] 같은 오류를 세 번 넘게 고치려 했다 → Risk
- [ ] 한 Epic에서 열린 Bug가 3개를 넘었다 → Risk
- [ ] Charter의 Stop Condition에 해당한다 → Risk. 멈추고 사람이 정한다
- [ ] Assumption List에 없는 가정이 새로 필요하다 → Assumption List에 더한다
- [ ] Stop Rule에 닿았다 → 진행을 멈춘다(12절)

## 7. DoD (Issue 마무리)

- PR Report: [`README.md`](README.md) 3.2를 따릅니다.
- Retrospective: `docs/journey.md`에 사람이 먼저 씁니다.
  - [ ] 잘 안 된 것. 없으면 "없음", 쓰지 못했으면 "생략"이라고 적습니다. 둘은 다릅니다
  - [ ] 알게 된 것

---

## 8. Release와 branch

### 8.1 Release
- Epic이 끝나면 main에 tag를 붙이고 GitHub Release를 만듭니다.
- tag 번호는 Epic 번호가 아니라 Release를 끝낸 순서로 붙입니다. 예: Epic 1(MVP)은 `v0.1.0`, Epic 2를 2a와 2b로 나눴다면 2a는 `v0.2.0`, 2b는 `v0.3.0`.
- release note에는 Epic 이름, 닫힌 Issue 목록, Retrospective 링크를 적습니다. tag 번호와 Epic 번호가 달라도 어느 Epic인지 알 수 있게 하기 위해서입니다.
- Release는 branch가 아니라 main 위의 tag입니다. tag는 Epic이 끝난 시점을 표시합니다.

### 8.2 branch (GitHub Flow)

```text
main ─●──●──●──●──●──────●──●──●──●──●──→
      #11 #12 #13 #14 #15  #21 #22 #23 #24 #25
                       ↑                    ↑
                  tag v0.1.0           tag v0.2.0
```

- branch는 Issue 하나에 하나씩 만듭니다. main에서 만들고, PR로 main에 합친 뒤 지웁니다.
- Epic branch와 Release branch는 만들지 않습니다. 한쪽에 모아 두었다가 한 번에 합치면, 떨어져 있던 만큼 충돌이 커지기 때문입니다.
- Spike branch는 merge하지 않습니다(11절).
- main은 언제나 동작하는 상태로 둡니다. User Story는 그 자체로 동작하고 test를 통과해야 merge합니다. 아직 쓰면 안 되는 기능은 화면에 연결하지 않은 채로 둡니다.

### 8.3 hotfix (이미 낸 버전을 급히 고칠 때)
main에는 이미 다음 Epic의 작업이 일부 들어 있을 수 있습니다. 그래서 이때만 tag에서 branch를 만듭니다.

```text
main ─●──●──●──●──●──────●──●──●───────●──→
                       ↑         \         ↑
                    v0.1.0        \     main에도 같은 수정을 넣는다
                       \           \
                        └─ hotfix ─●── tag v0.1.1
```

1. tag `v0.1.0`에서 hotfix branch를 만듭니다.
2. 고친 뒤 tag `v0.1.1`을 붙입니다.
3. 같은 수정을 main에도 넣습니다. 넣지 않으면 다음 Release에서 같은 Bug가 다시 나옵니다.

---

## 9. session

- session은 Retrospective를 마친 뒤에만 바꿉니다.
- 새 session은 [`README.md`](README.md) 3.4의 Five-line Check를 합니다. 셋째 줄에는 켜져 있는 Add-on을 모두 적습니다.

## 10. 끝

- MVP 도달: 첫 Release가 끝난 것이고, 프로젝트가 끝난 것은 아닙니다. Release Planning을 열어 다음 Epic으로 갈지, 여기서 마칠지 정합니다.
- [ ] Done: Epic List의 마지막 Epic까지 마쳤거나, Release Planning에서 "여기까지"로 정했다. 남은 Epic은 "하지 않음"으로 표시한다(3절)
- [ ] Archive: 더 진행하지 않는다. 배운 것을 마지막 Retrospective에 남긴다

---

## 11. Add-on (처리 절차 확인 모듈)

Add-on은 **문제가 생겼을 때 꺼내 쓰는 처리 절차**입니다. 늘 돌아가는 기능이 아니어서, 문제가 없으면 켜지 않습니다. 단순한 프로젝트는 한번도 켜지 않고 끝날 수 있습니다.

- AI는 켜야 할 상황을 보면 어떤 Add-on을 왜 켜야 하는지 알리고 멈춥니다. 동작여부는 사람이 정합니다.
- 할 일이 끝나면 끕니다.

| Add-on | 하는 일 | 끄는 때 |
|---|---|---|
| Blocker | `blocked` label을 붙이고 무엇을, 누구를, 언제까지 기다리는지 적습니다. 그동안 다른 Issue를 하나 진행합니다(4.3). 진행할 Issue가 없으면 Release Planning을 엽니다. 개수 제한은 Stop Rule(12절)을 따릅니다 | 풀리면 label을 떼고 이어서 합니다 |
| Spike | 확인할 질문, 끝나는 기준, timebox를 정한 Issue 하나로 만듭니다. 따로 branch에서 하고 merge하지 않습니다. 결과는 결정 기록으로 남깁니다. 근거가 되는 결과물(측정값, 설정 예)은 짧으면 결정 기록의 "근거와 참고자료"에 적고, 파일이면 `docs/evidence/<결정 ID>/`에 둡니다. `records/` 안에는 두지 않습니다. 기록 파일은 이름이 ID와 같아야 하기 때문입니다(00.common §7.5). 큰 원본(로그, 화면 캡처 여러 장)은 Learning 공간에 둡니다. 비밀값과 실제 주소는 저장소에 넣지 않습니다. 마치면 branch를 지웁니다 | timebox가 지나거나 답이 나오면 닫습니다 |
| Decision Candidate | AI가 결정 후보(`proposed`)를 씁니다. 찾아본 기존 결정과 바뀌는 것을 함께 적고, `decision-needed` label을 붙입니다. 결정이 나기 전에는 그 부분을 시작하지 않습니다 | 사람이 결정하면 끝납니다 |
| Assumption List | AI가 5W2H 표를 만들고 칸마다 "요청", "가정", "빈칸"으로 표시합니다. 사람은 "가정"만 확인하고 "빈칸"은 직접 채웁니다. 확인한 표로 Scenario와 test를 만듭니다 | 표를 확인하면 끝납니다. 새 가정이 생기면 다시 켭니다 |
| Release Planning | Decision Candidate와 Blocker부터 봅니다. Epic List에서 다음 Epic을 고르고 `docs/plan.md`에 적습니다. Epic Issue를 열고, Release Goal과 Acceptance Criteria를 정하고, 이번에 할 Issue를 고릅니다. 마지막으로 "이번 Release가 실패한다면 이유는?"을 묻습니다(Pre-mortem) | Release가 끝나면 끝납니다 |
| Backlog (`docs/backlog.md`) | Release Planning 때만 채웁니다. 이번 Release에서 할 Issue만, 크기 기준(4.4) 안에서 넣습니다. Release 중에는 Release Goal에 꼭 필요한 것만 더합니다. 넣고 순서를 정하는 것은 사람입니다 | 비면 끕니다. Release가 끝날 때 남은 것은 다음으로 넘길지 버릴지 정합니다 |
| Risk Register (`docs/risks.md`) | Risk의 신호를 셀 수 있는 사실로 적고 대응을 정합니다. Stop Condition에 해당하면 멈추고, 계속할지, 목표를 바꿀지, Archive할지 정해 결정 기록으로 남깁니다 | 신호가 사라지거나 결정이 나면 "닫힘"으로 표시합니다 |

## 12. Stop Rule

| 기준 | 수 | 그다음 |
|---|---|---|
| `blocked` Issue | 3개 | Claude Code가 진행을 멈춥니다. Release Planning을 열어 기다릴지, 목표를 바꿀지, Archive할지 정합니다 |
| Retrospective 생략 | 3번 연속 | Claude Code가 진행을 멈춥니다. 밀린 Retrospective를 쓰거나, 생략한 이유를 적은 뒤 다시 시작합니다 |

## 13. 문서

Charter는 고정하고, 나머지는 쌓아 갑니다. 지난 내용은 지우거나 고치지 않습니다.

| 문서 | 언제 생기나 | 어떻게 늘어나나 |
|---|---|---|
| `docs/plan-baseline.md` | 시작할 때 | 고정 (Charter) |
| `docs/plan.md` | 시작할 때 | Release마다 절이 하나씩 늘어납니다. 맨 위의 "Version Moon / 현재 Release / 현재 Issue"만 바뀝니다 |
| `docs/journey.md` | 시작할 때 | Issue와 Release마다 Retrospective가 늘어납니다 |
| `records/07.decision/` | 시작할 때 | 결정마다 파일이 늘어납니다. 이전 결정은 고치지 않습니다 |
| `docs/backlog.md` | Backlog를 켤 때 | Release마다 채우고 비웁니다 |
| `docs/risks.md` | Risk Register를 켤 때 | Risk가 늘어나고 닫힙니다 |
| `docs/evidence/<결정 ID>/` | Spike 결과물이 생길 때 | 결정마다 폴더가 늘어납니다. 고치지 않습니다 |

---

## 14. 용어 설명

뜻과, 일반 Agile과 다른 점만 적었습니다. 규칙과 숫자는 본문을 따릅니다.

| 용어 | 뜻 | 일반 Agile과 다른 점 |
|---|---|---|
| Charter (헌장) | 프로젝트에 하나 두는 고정 문서 | Product Vision의 역할 |
| Product Goal (제품 목표) | 누구를 위해, 무엇을 만들어, 어떤 문제를 푸는가 | |
| Out of Scope (하지 않는 것) | 이 프로젝트에서 만들지 않는 것 | |
| MVP (최소 제품) | 첫 Release가 끝났을 때 쓸 수 있는 상태 | 기능 목록이 아니라 상태로 씁니다. 프로젝트의 끝은 아닙니다 |
| Epic | 큰 그림의 한 칸 | 여기서는 Epic 하나가 Release 하나입니다. 일반적으로는 여러 Release에 걸치기도 합니다 |
| Epic List (큰 그림) | Learning에서 결정한 Epic 목록. 결정된 방향 | Roadmap이라고 부르지 않습니다. Roadmap은 보통 계속 바뀌는 것으로 쓰이기 때문입니다 |
| Epic Issue | Release 하나를 묶는 GitHub Issue | 진행 중인 Issue로 세지 않습니다 |
| Sub-issues (하위 Issue) | GitHub에서 Issue 아래에 자식 Issue를 연결하는 기능 | Milestone은 역할이 겹쳐 쓰지 않습니다 |
| Release (릴리스) | Epic 하나를 만드는 단위 | |
| Release Planning (릴리스 계획) | 다음 Epic을 고르고 이번에 할 Issue를 정하는 때 | 정해진 주기 없이 필요할 때 엽니다 |
| Release Goal (릴리스 목표) | 이번 Release가 끝났을 때의 상태 | |
| Backlog (백로그) | 이번 Release에서 처리할 Issue 목록 | 쌓아 두는 목록이 아닙니다 |
| Issue | Estimate 안에 끝나는 일 하나 | Epic을 대신하지 않습니다 |
| User Story | 기능을 만드는 Issue | 일반 Agile과 같습니다 |
| Bug | Acceptance Criteria대로 동작하지 않는 것을 고치는 Issue | |
| Walking Skeleton (첫 Issue) | 처음부터 끝까지 한 번 이어지는 가장 작은 기능 | |
| DoR (Definition of Ready, 시작 점검) | Issue를 시작하기 전에 갖출 것 | |
| Acceptance Criteria (끝났다는 기준) | 끝났다고 판단하는 기준 | |
| Estimate (예상 기간) | Issue에 걸릴 것으로 보는 기간 | 마감이 아닙니다. Story Point는 쓰지 않습니다 |
| DoD (Definition of Done, 완료 정의) | Issue를 마무리할 때 갖출 것 | |
| PR Report (PR 보고) | AI가 쓰고 사람이 검토하는 PR 보고 | |
| Retrospective (회고) | Issue와 Release가 끝날 때 돌아보는 기록 | 회의가 아니라 `docs/journey.md`의 짧은 기록입니다 |
| Sprint | 쓰지 않습니다 | 정해진 주기가 없습니다 |
| Watch (진행 중 확인) | 문제의 신호를 찾아 알리는 역할 | 고치거나 판단하지 않습니다. 화재 감지기처럼 알리기만 합니다 |
| Add-on (필요할 때 켜는 절차) | 문제가 생겼을 때 꺼내 쓰는 처리 절차 | 늘 돌아가는 기능이 아닙니다 |
| Blocker (막힌 일) | 밖의 무언가를 기다려야 해서 진행할 수 없는 Issue | 모르는 것, 하기 싫은 것은 Blocker가 아닙니다 |
| Spike (확인 작업) | 모르는 것을 확인하는 Issue | PoC와 같은 뜻입니다 |
| Decision Candidate (결정 후보) | AI가 쓰고 사람이 결정하는 결정 기록 초안 | |
| Assumption List (가정 목록) | AI가 요청의 빈칸을 5W2H로 드러낸 표 | |
| Scenario (시나리오) | 사람이 읽을 수 있게 쓴 확인할 상황 | Acceptance Test라고도 합니다 |
| Risk (위험) | 그대로 두면 프로젝트를 멈추게 할 수 있는 이슈 | 일어날 수 있는 모든 일이 아니라, 멈출 사유가 되는 것만 다룹니다 |
| Risk Register (위험 목록) | Risk와 그 신호, 대응, 상태를 적는 문서 | |
| Stop Condition (멈출 조건) | Charter에 미리 적어 두는 멈출 사유 | |
| Stop Rule (멈춤 기준) | 정해 둔 수에 닿으면 Claude Code가 진행을 멈추는 기준 | Lean의 Stop-the-line과 같은 생각입니다 |
| Pre-mortem (사전 부검) | "실패한다면 이유는?"을 먼저 묻는 방법 | |
| Five-line Check (다섯 줄 확인) | 새 session이 작업 전에 현재 상태를 다섯 줄로 말하는 것 | |
| tag | main의 한 시점에 붙이는 이름 | |
| GitHub Release | tag에 release note를 붙여 낸 버전을 기록하는 기능 | 일의 단위인 Release와는 다릅니다 |
| hotfix | 이미 낸 버전을 급히 고치는 것 | main이 아니라 tag에서 branch를 만드는 유일한 경우입니다 |
| Done / Archive (완료 / 보관) | 프로젝트의 끝 | Archive는 배운 것을 남기고 멈추는 것입니다 |
