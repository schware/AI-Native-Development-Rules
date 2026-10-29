# AI Native Development Rules

AI Agent와 함께 개발할 때 **AI의 제안과 사람의 결정 사이에 경계를 세우기 위한** 규칙과 프레임워크입니다.

## 왜 만들었나

AI Agent 과 함께 작업을 진행해야 하는 시대에 최소한의 규칙을 만들어야 하는 것에 대한 학습을 찾기 위한 작업이다. 
AI Agent 과 작업에서의 문제점 

- AI가 내놓은 답이 정답처럼 보여 그대로 넘어간 적이 많다.
- 문제가 드러나면 처음부터 다시 만드는 일이 반복된다.
- 결정의 근거는 AI Agent 채팅 속에만 묻혀서 다시 찾으려면 대화를 전수 조사 해야 한다.
- 대화를 전수 조사 하더라도 결정에 대한 부분은 사소한 단어가 결정의 근거가 된다.

이 저장소는 그 경험에서 출발한다. 결정을 드러내고 기록하는 약속을 하나씩 만들어 가는 과정을 담어 가려고 한다.

## 방향성

이 규칙은 생각을 설계하는 일을 돕습니다. 목표는 시간이 흘러도 살아남는 시스템입니다.

무엇을 만들든 다음 세 가지를 묻습니다.

- 기술적으로 맞는가
- 유지보수가 가능한가
- 10년 뒤에도 괜찮은가

AI Agent과 작업하는 것이 제품을 찍어내는 것이 아닌 이후 작업하기 위한 것을 목표로 해야 한다.

## 현재 버전

`v0.5.0` (초안). `0.x` 버전은 실험과 초안 단계입니다(00.common §11.4).

## 시작하기

새 프로젝트를 이 규칙으로 시작하려면 [`project-starter/START.md`](project-starter/START.md)를 따릅니다.

## 구성

| 경로 | 내용 |
|---|---|
| [`specification/`](specification/) | 명세. 지금 따르는 기준입니다 |
| [`specification/00.common/`](specification/00.common/) | 모든 영역에 공통인 규칙 |
| [`specification/07.decision/`](specification/07.decision/) | 결정 기록 규칙 |
| `specification/01~06, 08` | 아직 비어 있습니다. 필요해지면 작성합니다 |
| [`project-starter/`](project-starter/) | 새 프로젝트를 시작할 때 복사하는 파일과 예시 |
| [`docs/`](docs/) | 실제 프로젝트에 적용하며 모은 경험과 다음 버전 후보 |
| [`ai-native-development-framework-v03/`](ai-native-development-framework-v03/) | 명세 이전의 프레임워크 문서. 배경과 개념을 참고하는 용도이며 기준은 아닙니다 |
| [`ai-native-development-framework-v03/DECISION-LOG.md`](ai-native-development-framework-v03/DECISION-LOG.md) | 명세 이전의 결정 이력. 새 형식으로 정리할 예정입니다 |
| [`ai-native-development-framework-v03/FULL-CONTEXT.md`](ai-native-development-framework-v03/FULL-CONTEXT.md) | 대화가 발전해 온 과정 전체 |
| [`ai-native-development-framework-markdown-sets/`](ai-native-development-framework-markdown-sets/) | 이전 버전 (Human/Agent 세트). 이력으로 보관 |
| [`ai-native-development-framework-conversation-evolution.md`](ai-native-development-framework-conversation-evolution.md) | 초기 대화 발전 기록. 이력으로 보관 |

## 상태

작업 중인 초안(Working Draft)입니다. 규칙은 `specification/`에서 관리하고, 실제 프로젝트에 적용해 보면서 다음 버전으로 발전시킵니다.
