# 스킬: Final Backlog (백로그 확정)

> **역할:** PM / Tech Lead
> **선행 조건:** 반드시 `skills/0_process_concerns.md`를 먼저 읽는다. 규칙 충돌 시 0번 규칙 우선.

## 🎯 목표
- BACKLOG_DRAFT를 기반으로 최종 백로그(Sprint별 Task + DoD)를 확정한다.

## 📥 입력
- WORK_CYCLE_ROOT (`./docs/improvement` 우선, 없으면 최신 `./docs/*_done`)
- `${WORK_CYCLE_ROOT}/final/*`
- (권장) `${WORK_CYCLE_ROOT}/3/BACKLOG_DRAFT.md`

## 📤 출력
- `${WORK_CYCLE_ROOT}/final/BACKLOG.md`

## 🚨 사전 확인
- `${WORK_CYCLE_ROOT}/final/TRD.md` 상태 확인
- 상태가 `BLOCKED:*`이면 Sprint 백로그 확정 금지
- BLOCKED 사유/질문/영향만 정리
- `BACKLOG_DRAFT.md`가 없으면 상태: `BLOCKED: BACKLOG_DRAFT_MISSING`

## 📋 형식
```
Epic
 └ Story
    └ Task + Definition of Done
```

## 🚫 규칙
- Enhancement 범위 기준으로 MVP / Post-MVP 분리
- `BACKLOG_DRAFT.md`를 입력으로 받아 우선순위/스프린트만 "확정"한다
- Sprint 1 기준 우선순위 확정(초안이 아닌 확정본)
- 모든 Task DoD에 아래 항목 포함:
  - 기존 기능 회귀 없음
  - TRD Stack Contract 위반 없음
  - 범위 외 변경 없음

## 🔗 하니스 연동 (랄프 루프 사용 시)
- 완료 후 `context/3_checklist.md`의 BACKLOG 항목을 `[x]`로 마킹
- `context/2_context_note.md`에 Sprint 분할 확정 결과 기록
