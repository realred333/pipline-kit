# 스킬: Final Merge (문서 통합)

> **역할:** 문서 통합 담당
> **선행 조건:** 반드시 `skills/0_process_concerns.md`를 먼저 읽는다. 규칙 충돌 시 0번 규칙 우선.

## 🎯 목표
- 1차(TRD), 2차(API), 3차(PLAN) 문서들을 하나의 최종(final) 문서 세트로 통합한다.
- 중복 제거, TBD 정리, 충돌 해결을 수행한다.

## 📥 입력
- `TRACK` (기본값: `MAJOR`, 옵션: `MINOR`)
- WORK_CYCLE_ROOT (`./docs/improvement` 우선, 없으면 최신 `./docs/*_done`)
- `${WORK_CYCLE_ROOT}/1/*`
- (선택) `${WORK_CYCLE_ROOT}/2/*`
- (선택) `${WORK_CYCLE_ROOT}/3/*`

## 📤 출력
- `${WORK_CYCLE_ROOT}/final/TRD.md`
- `${WORK_CYCLE_ROOT}/final/API_SPEC.md`
- `${WORK_CYCLE_ROOT}/final/PLAN.md`
- `${WORK_CYCLE_ROOT}/final/OPEN_QUESTIONS.md`

## 🔧 작업
- 중복 제거
- TBD 정리
- 충돌 정리
- 최종 문서 생성

## 📌 MINOR 트랙 처리
- `TRACK=MINOR`이면 `${WORK_CYCLE_ROOT}/2/*`, `${WORK_CYCLE_ROOT}/3/*`가 없어도 진행한다.
- 누락된 경우 아래처럼 placeholder 문서를 만든다:
  - `final/API_SPEC.md`: `Status: SKIPPED (NO_API_CHANGE 또는 NOT_PROVIDED)` + 근거
  - `final/PLAN.md`: `Status: SKIPPED (NOT_PROVIDED)` 또는 TRD의 Sprint Scope를 요약

## 🚫 하드 규칙
- 스택/인프라/인증/DB/테스트 충돌은 임의 선택 금지
- 충돌 시 `OPEN_QUESTIONS.md`에 기록하고 상태를 `BLOCKED: STACK_CONFLICT`로 둔다
- 질문을 사용자에게 전달하고 답변 전까지 `READY_FOR_IMPLEMENTATION` 확정 금지
- final TRD에 Stack Contract와 상태를 반드시 포함
- final TRD에 `CYCLE_LABEL`이 있으면 유지(없으면 `OPEN_QUESTIONS.md`에 기록)
- final API_SPEC/PLAN은 final TRD 상태와 정합되어야 함

## 🔗 하니스 연동 (랄프 루프 사용 시)
- 완료 후 `context/3_checklist.md`의 MERGE 항목을 `[x]`로 마킹
- `context/2_context_note.md`에 통합 결과 및 미해결 충돌 기록
