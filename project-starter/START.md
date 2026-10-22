# 프로젝트 시작 템플릿

새 프로젝트를 AI Native Development Rules에 따라 시작하기 위한 파일 모음이다.

- `files/` 안의 내용을 새 프로젝트 저장소의 루트에 그대로 복사한다.
- 이 문서(`START.md`)는 복사하지 않는다.
- 템플릿은 명세와 같은 Git Tag로 버전을 관리한다. 프로젝트는 시작할 때 사용한 Tag를 `project.yaml`의 `git_ref`에 적는다.

## files/ 구성

| 파일 | 역할 | 근거 |
|---|---|---|
| `project.yaml` | 프로젝트 ID, 따르는 명세와 버전, 기록 경로, 역할 | 00.common §6.4 |
| `.gitattributes` | 줄바꿈을 LF로 통일 | 00.common §6.8 |
| `records/07.decision/` | 공식 결정 기록을 두는 곳 | 00.common §6.8 |
| `current-state.md` | 지금 유효한 규칙. 줄마다 근거 결정 ID를 붙인다 | 07.decision §8.7 |
| `CLAUDE.md` | AI Agent가 작업 전에 읽을 것과 지킬 것 | 00.common §12.2 |
| `.github/pull_request_template.md` | 반영 전에 사람이 확인할 체크리스트 | 00.common §12.1, §8.5 |
| `templates/decision.md` | 결정 기록의 빈 양식 | 07.decision §6 |

`templates/decision.md`를 `records/` 밖에 두는 이유는, `records/` 안의 파일은 이름이 기록 ID와 같아야 하기 때문이다(00.common §7.5).

## examples/ (복사하지 않음)

다 채운 기록의 예시를 둔다. 빈 양식을 채울 때 참고한다.

| 파일 | 보여 주는 것 |
|---|---|
| `EXAMPLE001-D001.md` | Claude Code와 함께 만든 결정 기록. AI가 초안과 추천을 쓰고(`drafted_by: ai_agent`, `proposed_by: ai_agent`), 사람이 내용을 확인하고(`confirmed_by`) 추천안을 그대로 채택해 결정한(`adoption: as_proposed`, `decided_by`) 경우이다 |

## 시작하는 방법

새 프로젝트 저장소의 폴더에서 PowerShell로 실행한다.

### 1. 사용할 버전의 템플릿과 명세 가져오기

```powershell
git clone --depth 1 --branch v0.1.0 https://github.com/schware/AI-Native-Development-Rules.git "$env:TEMP\anr-v0.1.0"
```

### 2. 템플릿 파일 복사

```powershell
Copy-Item -Recurse -Force "$env:TEMP\anr-v0.1.0\project-starter\files\*" .
```

### 3. 명세의 읽기 전용 사본 만들기

AI Agent는 이 사본을 읽는다(`CLAUDE.md` 참고). 사본은 직접 고치지 않고, 명세 버전을 올릴 때만 다시 복사한다(00.common §11.5).

```powershell
New-Item -ItemType Directory -Force .framework
```

```powershell
Copy-Item -Recurse -Force "$env:TEMP\anr-v0.1.0\specification" .framework\
```

### 4. 빈칸 채우기

`project.yaml`의 `<PROJECT_ID>`, `<PROJECT_NAME>`, `<PERSON_ID>`를 채운다. `templates/decision.md`의 `<PROJECT_ID>`도 같은 값으로 바꾼다.

### 5. 첫 commit

```powershell
git add -A
```

```powershell
git commit -m "Start project from AI Native Development Rules v0.1.0"
```

### 6. 첫 결정 기록

`templates/decision.md`를 복사해 `records/07.decision/<PROJECT_ID>-D001.md`를 만들고 첫 결정을 기록한다. 결정이 `decided`가 되어 지금 유효한 규칙이 생기면 `current-state.md`에도 같은 Pull Request에서 추가한다.

## 명세 버전을 올릴 때

1. 새 Tag로 1단계와 3단계를 다시 실행해 `.framework/`를 바꾼다.
2. `project.yaml`의 `git_ref`를 새 Tag로 바꾼다.
3. 바뀐 규칙이 기존 기록과 `current-state.md`에 영향을 주는지 확인한다(00.common §11.6).
