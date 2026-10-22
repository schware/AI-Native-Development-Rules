# 프로젝트 시작 템플릿

새 프로젝트를 AI Native Development Rules에 따라 시작하기 위한 파일 모음이다.

- `files/` 안의 내용을 새 프로젝트 저장소의 루트에 그대로 복사한다.
- 이 문서(`START.md`)는 복사하지 않는다.
- 템플릿은 명세와 같은 Git Tag로 버전을 관리한다. 프로젝트는 시작할 때 사용한 Tag를 `project.yaml`의 `git_ref`에 기준 버전으로 적는다.
- 복사한 명세는 프로젝트의 규칙이 되며, 프로젝트 안에서 발전시킨다(00.common §11.5).

```text
기준 저장소 v0.1 ──복사──→ 프로젝트 A (v0.1 기준, A의 규칙으로 발전)
               └──복사──→ 프로젝트 B (v0.1 기준, B의 규칙으로 발전)

기준 저장소 v0.2 ──확인 후 적용──→ 프로젝트 A (v0.2 기준)
               └──적용하지 않음──→ 프로젝트 B (v0.1 기준 유지)
```

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
git clone --depth 1 --branch v0.2.0 https://github.com/schware/AI-Native-Development-Rules.git "$env:TEMP\anr-v0.2.0"
```

### 2. 템플릿 파일 복사

```powershell
Copy-Item -Recurse -Force "$env:TEMP\anr-v0.2.0\project-starter\files\*" .
```

### 3. 프로젝트의 규칙 사본 만들기

이 사본이 프로젝트의 규칙이 되며, AI Agent도 이 사본을 읽는다(`CLAUDE.md` 참고). 고치는 방법은 아래 "프로젝트에서 규칙을 고칠 때"를 따른다.

```powershell
New-Item -ItemType Directory -Force .framework
```

```powershell
Copy-Item -Recurse -Force "$env:TEMP\anr-v0.2.0\specification" .framework\
```

### 4. 빈칸 채우기

`project.yaml`의 `<PROJECT_ID>`, `<PROJECT_NAME>`, `<PERSON_ID>`를 채운다. `templates/decision.md`의 `<PROJECT_ID>`도 같은 값으로 바꾼다.

### 5. 첫 commit

```powershell
git add -A
```

```powershell
git commit -m "Start project from AI Native Development Rules v0.2.0"
```

### 6. 첫 결정 기록

`templates/decision.md`를 복사해 `records/07.decision/<PROJECT_ID>-D001.md`를 만들고 첫 결정을 기록한다. 결정이 `decided`가 되어 지금 유효한 규칙이 생기면 `current-state.md`에도 같은 Pull Request에서 추가한다.

## 프로젝트에서 규칙을 고칠 때

1. 무엇을 왜 바꾸는지 결정 기록(`records/07.decision/`)으로 남긴다. AI Agent는 결정 후보까지만 작성하고, 결정은 사람이 한다.
2. 결정이 `decided`가 되면 `.framework/specification/`의 해당 규칙을 고친다.
3. 규칙을 고치는 커밋에 그 결정 ID를 `Record-Refs`로 적는다.

이 기록이 있어야 새 기준 버전이 나왔을 때 프로젝트에서 바꾼 규칙을 찾을 수 있고, 기준 저장소에 반영할 때도 근거가 된다.

## 새 기준 버전이 나왔을 때

1. 기준 저장소에서 두 버전의 차이를 확인한다. 예: `https://github.com/schware/AI-Native-Development-Rules/compare/v0.2.0...v0.3.0`
2. 적용할지 사람이 결정하고, 결정 기록으로 남긴다. 적용하지 않으면 여기서 끝난다.
3. 적용한다면 새 버전을 임시 폴더로 가져온다.

   ```powershell
   git clone --depth 1 --branch v0.3.0 https://github.com/schware/AI-Native-Development-Rules.git "$env:TEMP\anr-v0.3.0"
   ```

4. 프로젝트의 사본과 새 버전을 비교한다. **새 버전으로 그대로 덮어쓰면 프로젝트에서 고친 규칙이 사라진다.**

   ```powershell
   git diff --no-index .framework\specification "$env:TEMP\anr-v0.3.0\specification"
   ```

5. 프로젝트에서 고친 규칙 중 남길 것을 정하고, 새 버전의 변경을 사본에 반영한다.
6. `project.yaml`의 `git_ref`를 새 버전으로 바꾸고, 바뀐 규칙이 기존 기록과 `current-state.md`에 영향을 주는지 확인한다.

## 프로젝트의 개선을 기준 저장소에 반영할 때

프로젝트에서 발전시킨 규칙을 다른 프로젝트에서도 쓰고 싶으면, 기준 저장소(AI-Native-Development-Rules)에서 Claude Code에 반영을 요청한다. 그 규칙을 고친 프로젝트의 결정 기록을 근거로 함께 알려 준다. 반영한 뒤에는 새 버전 Tag를 만든다.
