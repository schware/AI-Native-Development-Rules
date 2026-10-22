## 변경 내용

## 관련 기록

Record-Refs:

## 체크리스트 (00.common §12.1)

- [ ] 파일 이름과 내부 `id`가 같다
- [ ] `id`가 중복되지 않는다
- [ ] 공통 필드(`id`, `title`, `status`, `created_at`, `drafted_by`, `issues`)가 있다
- [ ] `title`과 본문 첫 제목이 같다
- [ ] `status`가 허용된 값이다
- [ ] 참조한 기록이 존재한다
- [ ] `replaces`를 썼다면 대체된 결정을 `superseded`로 바꿨다
- [ ] AI가 쓴 내용은 `drafted_by`로 표시했다
- [ ] `proposed` 상태의 결정이 5개 이하다
- [ ] 결정이 `current-state.md`를 바꾸면 같은 Pull Request에서 함께 고쳤다

## 위험 등급과 독립 AI 검토 (00.common §12.3)

- risk_level:
- 독립 AI 검토: 필요 / 불필요
- 검토 결과: Blocking / Warning / Suggestion / No Issue
