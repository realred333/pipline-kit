# 스킬: Agent Plan (실행 계획 / QA 전략 / 백로그 초안)

> **역할:** Agent 3 — 실행 계획 / QA / 릴리즈 담당
> **선행 조건:** 반드시 `skills/0_process_concerns.md`를 먼저 읽는다. 규칙 충돌 시 0번 규칙 우선.

## 🎯 목표
- PRD와 TRD/API 문서를 바탕으로 구체적인 실행 계획, 테스트 전략, 백로그 초안을 수립한다.

## 📥 입력
- 최신 PRD (`PRD_REV{N}.md` 중 N 최대, 없으면 최신 `PRD_*.md`)
- 기존 코드베이스 전체 (read-only 분석)
- WORK_CYCLE_ROOT (새 사이클이면 `./docs/improvement`)

## 📤 출력
- `${WORK_CYCLE_ROOT}/3/PLAN.md`
- `${WORK_CYCLE_ROOT}/3/TEST_PLAN.md`
- `${WORK_CYCLE_ROOT}/3/RELEASE_CHECKLIST.md`
- `${WORK_CYCLE_ROOT}/3/BACKLOG_DRAFT.md`

## 🚨 진입 게이트
- `./docs/improvement`가 없으면 `./docs/improvement/{1,2,3,final}` 생성 후 진행
- 컨텍스트 미흡 시 `Status: BLOCKED: CONTEXT_REQUIRED`
- 핵심 스택 미결정 시 `Status: BLOCKED: STACK_DECISION_REQUIRED`
- 스택/아키텍처 충돌 시 `Status: BLOCKED: STACK_CONFLICT`

## 📋 PLAN.md 필수 항목
- Status
- 개선 목표 / 범위
- Epic / Story / Task
- Sprint 분할
- 리스크/의존성
- Stack Guardrail (기존 스택 유지 + 예외 승인 절차)

## 📋 BACKLOG_DRAFT.md 필수 항목
- Status
- Epic → Story → Task + Definition of Done
- Sprint 1 우선순위가 보이도록 정렬(초안)
- DoD 최소 포함:
  - 기존 기능 회귀 없음
  - TRD Stack Contract 위반 없음
  - 범위 외 변경 없음

## 📋 TEST_PLAN.md 필수 항목
- Status
- 단위/통합/E2E 전략
- 회귀 테스트 항목
- 변경 영향 기반 우선 테스트
- 스택 정합성 검증 항목

## 📋 RELEASE_CHECKLIST.md 필수 항목
- Status
- 배포 전 체크
- 롤백 절차
- 모니터링/알림
- Stack Contract 위반 검사

## 🚫 금지
- 신규 프로젝트 생성 계획
- PRD 근거 없는 신규 스택 제안

## 🔗 하니스 연동 (랄프 루프 사용 시)
- 완료 후 `context/3_checklist.md`의 PLAN 항목을 `[x]`로 마킹
- `context/2_context_note.md`에 Sprint 분할 요약 및 리스크 기록
