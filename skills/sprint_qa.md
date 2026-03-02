# 스킬: Sprint QA (스프린트 품질 검증)

> **역할:** Sprint QA 담당
> **선행 조건:** 반드시 `skills/0_process_concerns.md`를 먼저 읽는다. 규칙 충돌 시 0번 규칙 우선.
> **트리거:** 매 Sprint 구현 직후 반복 수행: `IMPLEMENT_SPRINT (Sprint N) → SPRINT_QA (Sprint N)`

## 🎯 목표
- 스프린트 구현 결과를 검증하고 에러/회귀/보안 취약점을 확인한다.
- PASS 시 다음 Sprint로, FAIL 시 원인을 기록하고 재시도한다.

## 📥 입력
- `TRACK` (기본값: `MAJOR`, 옵션: `MINOR`)
- `SPRINT_NUMBER` (예: 1, 2, 3...)
- (선택) `QA_ATTEMPT` (기본: 1)
- (선택) `MAX_QA_CYCLES_PER_SPRINT` (기본: 3)
- 전체 프로젝트
- WORK_CYCLE_ROOT (`./docs/improvement` 우선, 없으면 최신 `./docs/*_done`)
- (선택) `${WORK_CYCLE_ROOT}/final/*`
- (선택) `${WORK_CYCLE_ROOT}/final/BACKLOG.md`

## 📤 출력
- `${WORK_CYCLE_ROOT}/final/SPRINT{SPRINT_NUMBER}_RESULT.md`

## 📥 문서 소스 우선순위
- TRD: `${WORK_CYCLE_ROOT}/final/TRD.md`가 있으면 그걸 사용, 없으면 `${WORK_CYCLE_ROOT}/1/TRD.md`
- BACKLOG: `${WORK_CYCLE_ROOT}/final/BACKLOG.md` (MAJOR는 필수, MINOR는 선택)

## 📌 Sprint 범위 결정
- `TRACK=MAJOR`: BACKLOG의 `Sprint {SPRINT_NUMBER}` Task 기준으로 완료/잔여를 판단한다.
- `TRACK=MINOR`:
  - BACKLOG가 있으면 동일하게 사용한다.
  - BACKLOG가 없으면 TRD의 `Sprint {SPRINT_NUMBER} Scope` 기준으로 판단한다.

## 🚨 사전 검증 (하드 게이트)
- **무한루프 방지:**
  - `QA_ATTEMPT > MAX_QA_CYCLES_PER_SPRINT`이면 즉시 `FAIL_MAX_RETRIES`로 종료하고 원인/다음 액션을 기록
- TRD 상태 `READY_FOR_IMPLEMENTATION`
- Stack Contract 미결정(`<UNDECIDED>`) 없음
- 코드와 TRD 정합성 확인
- `TRACK=MAJOR`인데 BACKLOG가 없으면 QA를 `FAIL`로 종료하고 원인 기록
- 미충족 시 QA를 FAIL로 종료하고 원인 기록

## 🔧 작업 순서
1. Sprint {SPRINT_NUMBER} 결과 검증
2. 테스트 실행
3. 실패 수정
4. 재검증
5. 정합성 검증

## ✅ 체크 항목
- Sprint {SPRINT_NUMBER} Task 완료 여부
- 테스트 통과 여부
- 회귀 여부
- TRD Stack Contract 준수 여부
- 신규 스택/프레임워크 무단 도입 여부
- **보안 취약점 점검:** API Key, 비밀번호 등 하드코딩 여부
- **에러 처리 점검:** 예외 상황에 대한 적절한 처리가 되어 있는지

## 📋 SPRINT{N}_RESULT.md 필수 항목
- 상태 (PASS / FAIL)
- 완료 기능
- 테스트 결과
- 회귀 이슈
- 남은 Task
- 다음 Sprint 필요 여부
- 차단 이슈/질문

## 🔗 하니스 연동 (랄프 루프 사용 시)
- QA PASS 시 `context/3_checklist.md`의 Sprint N QA 항목을 `[x]`로 마킹
- QA FAIL 시 `context/2_context_note.md`에 실패 원인과 다음 시도 전략 기록
- 모든 Sprint 완료 후 → `skills/final_qa_release.md` (MAJOR) 또는 `skills/final_cleanup.md` (MINOR)
