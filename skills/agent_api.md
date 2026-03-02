# 스킬: Agent API (API / 데이터 모델 설계)

> **역할:** Agent 2 — API / Data Model 담당
> **선행 조건:** 반드시 `skills/0_process_concerns.md`를 먼저 읽는다. 규칙 충돌 시 0번 규칙 우선.

## 🎯 목표
- 기존 API/DB 모델을 우선 재사용하고 필요한 변경만 설계한다.
- PRD에 없는 신규 기능/스택 도입 금지.

## 📥 입력
- 최신 PRD (`PRD_REV{N}.md` 중 N 최대, 없으면 최신 `PRD_*.md`)
- 기존 코드베이스 전체 (read-only 분석)
- WORK_CYCLE_ROOT (새 사이클이면 `./docs/improvement`)

## 📤 출력
- `${WORK_CYCLE_ROOT}/2/API_SPEC.md`
- `${WORK_CYCLE_ROOT}/2/DATA_MODEL.md`
- `${WORK_CYCLE_ROOT}/2/ERRORS.md`

## 🚨 진입 게이트
- `./docs/improvement`가 없으면 `./docs/improvement/{1,2,3,final}` 생성 후 진행
- 컨텍스트 미흡 시 `Status: BLOCKED: CONTEXT_REQUIRED`
- 핵심 스택 미결정 시 `Status: BLOCKED: STACK_DECISION_REQUIRED`
- 기존 모델과 충돌 + 마이그레이션 전략 부재 시 `Status: BLOCKED: STACK_CONFLICT`

## 📋 API_SPEC.md 필수 항목
- Status
- As-Is API 요약
- 변경/추가 Endpoint 목록 (변경 이유 포함)
- Method / Path / Request / Response 예시
- 인증/권한 규칙
- 하위호환성(Backward Compatibility) 영향
- Open Questions

## 📋 DATA_MODEL.md 필수 항목
- Status
- As-Is 데이터 모델 요약
- 변경 대상 엔티티/필드/관계
- 마이그레이션 필요 여부
- 롤백/데이터 보존 고려사항
- Open Questions

## 📋 ERRORS.md 필수 항목
- Status
- 에러 코드 테이블
- 사용자 메시지 / 개발자 메시지
- 재시도 가능 여부
- 공통 에러 포맷

## 🔗 하니스 연동 (랄프 루프 사용 시)
- 완료 후 `context/3_checklist.md`의 API 항목을 `[x]`로 마킹
- `context/2_context_note.md`에 API 변경사항 요약 및 오픈 이슈 기록
