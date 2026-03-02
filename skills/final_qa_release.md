# 스킬: Final QA Release (최종 QA / 릴리즈 판정)

> **역할:** 최종 QA / Release 담당
> **선행 조건:** 반드시 `skills/0_process_concerns.md`를 먼저 읽는다. 규칙 충돌 시 0번 규칙 우선.
> **트리거:** 모든 Sprint 종료 후 1회 수행 (MAJOR 트랙만 필수)

## 🎯 목표
- 전체 프로젝트에 대한 최종 QA를 수행하고 릴리즈 가능 여부를 판정한다.

## 📥 입력
- (선택) `RELEASE_ATTEMPT` (기본: 1)
- (선택) `MAX_RELEASE_CYCLES` (기본: 2)
- 전체 프로젝트
- WORK_CYCLE_ROOT (`./docs/improvement` 우선, 없으면 최신 `./docs/*_done`)
- `${WORK_CYCLE_ROOT}/final/*`

## 📤 출력
- `${WORK_CYCLE_ROOT}/final/RESULT.md`

## 🚨 사전 검증 (하드 게이트)
- **무한루프 방지:**
  - `RELEASE_ATTEMPT > MAX_RELEASE_CYCLES`이면 즉시 `NOT READY_MAX_RETRIES`로 기록하고 종료
- final TRD 상태가 `READY_FOR_IMPLEMENTATION`
- Stack Contract 미결정(`<UNDECIDED>`) 없음
- 코드와 TRD Stack Contract 정합성 확인
- 조건 미충족 시 릴리즈 상태를 `NOT READY`로 기록

## 🔧 작업 순서
1. 전체 테스트 실행
2. 실패 수정
3. 재검증
4. 스택/아키텍처 정합성 최종 검증
5. RESULT.md 작성
6. `FINAL_CLEANUP` 단계에서 사용할 리네이밍 대상(PRD `REV` 승격, docs 폴더명)을 RESULT.md에 명시

## 📋 RESULT.md 필수 항목
- 상태 (READY / NOT READY)
- 완료 기능 요약
- 설치/실행 방법
- 남은 TODO
- 알려진 제약/주의사항
- 배포 준비 상태 + 이유
- TRD 대비 스택/아키텍처 정합성 (PASS / FAIL + 근거)
- 무단 신규 스택 도입 여부 (없음 / 있음 + 위치)
- 오픈 질문/차단 이슈
- 최종 정리 리네이밍 지시 (PRD `REV` 승격, docs 폴더명 정리 필요 여부)

## 🔗 하니스 연동 (랄프 루프 사용 시)
- READY 시 `context/3_checklist.md`의 FINAL QA 항목을 `[x]`로 마킹
- NOT READY 시 `context/2_context_note.md`에 원인과 다음 시도 전략 기록
