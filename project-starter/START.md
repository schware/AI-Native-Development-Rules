# 프로젝트 시작 템플릿

새 프로젝트를 AI Native Development Rules에 따라 시작하기 위한 파일 모음이다.

- 프로젝트는 이 저장소를 Git submodule로 `.framework/`에 연결하고, 특정 버전(Git Tag)을 가리킨다(00.common §11.5).
- 공통 규칙은 이 저장소에서만 고친다. 프로젝트는 submodule 안의 파일을 고치지 않고, 새 버전이 나오면 확인한 뒤 가리키는 버전을 옮긴다.
- 프로젝트에만 적용하는 규칙은 프로젝트의 `current-state.md`에 둔다.
- `files/` 안의 내용을 새 프로젝트 저장소의 루트에 복사해서 시작한다. 이 문서(`START.md`)는 복사하지 않는다.

```text
AI-Native-Development-Rules (규칙은 여기서만 고친다)
   v0.4 ──→ v0.5 ──→ v0.6
     ↑ submodule이 가리키는 버전
프로젝트 A: v0.4를 가리키며 진행 → 확인 후 v0.5로 옮김
프로젝트 B: v0.4를 계속 가리킴 (옮기지 않기로 결정)
```

## files/ 구성

| 파일 | 역할 | 근거 |
|---|---|---|
| `project.yaml` | 프로젝트 ID, 따르는 명세와 버전, 기록 경로, 역할 | 00.common §6.4 |
| `.gitattributes` | 줄바꿈을 LF로 통일 | 00.common §6.8 |
| `records/07.decision/` | 공식 결정 기록을 두는 곳 | 00.common §6.8 |
| `current-state.md` | 이 프로젝트에서 지금 유효한 규칙. 줄마다 근거 결정 ID를 붙인다 | 00.common §4, §11.5, 07.decision §8.7 |
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

새 프로젝트 저장소(이미 `git init` 또는 clone한 폴더)의 루트에서 PowerShell로 실행한다.

### 1. 이 저장소를 submodule로 연결

```powershell
git submodule add https://github.com/schware/AI-Native-Development-Rules.git .framework
```

### 2. 따를 버전 고르기

```powershell
git -C .framework checkout v0.4.0
```

### 3. 템플릿 파일 복사

```powershell
Copy-Item -Recurse -Force ".framework\project-starter\files\*" .
```

### 4. 빈칸 채우기

`project.yaml`의 `<PROJECT_ID>`, `<PROJECT_NAME>`, `<PERSON_ID>`를 채운다. `templates/decision.md`의 `<PROJECT_ID>`도 같은 값으로 바꾼다. `git_ref`가 2단계에서 고른 버전과 같은지 확인한다.

### 5. 첫 commit

```powershell
git add -A
```

```powershell
git commit -m "Start project from AI Native Development Rules v0.4.0"
```

### 6. 첫 결정 기록

`templates/decision.md`를 복사해 `records/07.decision/<PROJECT_ID>-D001.md`를 만들고 첫 결정을 기록한다. 결정이 `decided`가 되어 지금 유효한 규칙이 생기면 `current-state.md`에도 같은 Pull Request에서 추가한다.

## 다른 PC나 새 worktree에서 열 때

submodule은 자동으로 채워지지 않는다. `.framework/`가 비어 있으면 AI Agent가 규칙을 읽을 수 없다.

처음 clone할 때:

```powershell
git clone --recurse-submodules <프로젝트 저장소 주소>
```

이미 clone했거나 새 worktree를 만들었을 때:

```powershell
git submodule update --init
```

## 프로젝트에만 적용하는 규칙을 정할 때

1. 무엇을 왜 정하는지 결정 기록(`records/07.decision/`)으로 남긴다. AI Agent는 결정 후보까지만 작성하고, 결정은 사람이 한다.
2. 결정이 `decided`가 되면 `current-state.md`에 그 규칙을 결정 ID와 함께 적는다.
3. 같은 커밋에 그 결정 ID를 `Record-Refs`로 적는다.

`.framework/` 안의 파일은 고치지 않는다.

## 공통 규칙을 바꾸고 싶을 때

프로젝트에서 공통 규칙을 바꿀 필요를 발견하면, 이 저장소(AI-Native-Development-Rules)에서 Claude Code에 반영을 요청한다. 근거가 된 프로젝트의 결정 기록을 함께 알려 준다. 반영한 뒤에는 새 버전 Tag를 만들고, 프로젝트에서는 아래 "새 버전으로 옮길 때"를 따른다.

## 새 버전으로 옮길 때

1. 두 버전의 차이를 확인한다. 예: `https://github.com/schware/AI-Native-Development-Rules/compare/v0.4.0...v0.5.0`
2. 옮길지 사람이 결정하고, 결정 기록으로 남긴다. 옮기지 않으면 여기서 끝난다.
3. 새 버전을 가져온다.

   ```powershell
   git -C .framework fetch --tags
   ```

   ```powershell
   git -C .framework checkout v0.5.0
   ```

4. `project.yaml`의 `git_ref`를 같은 버전으로 바꾼다.
5. 바뀐 규칙이 기존 기록과 `current-state.md`에 영향을 주는지 확인한다.
6. commit한다. 2단계의 결정 ID를 `Record-Refs`로 적는다.

   ```powershell
   git add .framework project.yaml
   ```
