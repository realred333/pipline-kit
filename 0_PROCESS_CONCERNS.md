# 0. 필독 규칙 (Enhancement 공통: MINOR/MAJOR)

이 문서는 **기존 프로젝트 개선(Enhancement)** 파이프라인의 최상위 규칙이다.
다른 프롬프트를 실행하기 전에 반드시 먼저 읽고 준수한다.

> 프로젝트 시작(그린필드)인 `KICKOFF` 트랙은 이 문서가 아니라
> `0_KICKOFF_CONCERNS.md`를 사용한다.

## A. 작업 타입 고정
- 기본값은 `기존 프로젝트 개선(Enhancement)`이다.
- PRD 근거 없는 신규 프로젝트 생성/재구축(From Scratch) 금지.

## A-1. 트랙 선택 (게이트 강도)
- `TRACK=MAJOR`(기본): 하드 게이트 + 문서 풀세트(1/2/3/final) 기준.
- `TRACK=MINOR`: 문서/게이트를 완화할 수 있지만, 아래는 유지한다.
  - PRD 필수
  - Stack Contract는 `<UNDECIDED>` 없이 확정
  - Sprint 범위(작업 목록 + DoD)는 문서에 명시

## B. 범위 고정 (Scope Lock)
- 이번 라운드 In Scope만 수행한다.
- 진행 중 새 아이디어/요청은 즉시 구현하지 말고 `BACKLOG`에 기록한다.
- 범위 외 작업은 `OUT-OF-SCOPE`로 표시하고 승인 전 착수 금지.

## C. 컨텍스트 게이트
아래가 없으면 진행 금지:
- 접근 가능한 기존 코드베이스
- PRD(기본: 최신 `PRD_REV{N}.md`, 없으면 최신 `PRD_*.md`)
- 변경 대상 범위(In Scope)

미충족 시:
- 상태: `BLOCKED: CONTEXT_REQUIRED`
- 누락 항목 + 확인 질문만 출력

## D. 스택 결정 게이트
아래 항목은 `결정값 + 출처`가 필수:
- Frontend
- Backend 실행모델/프레임워크
- DB
- Auth
- 배포/인프라
- 테스트 도구

미결정 처리:
- PRD 명시값 우선
- PRD 미명시 시 기존 코드 검출값 우선
- 둘 다 없으면 `BLOCKED: STACK_DECISION_REQUIRED`

## E. 정합성 게이트
- PRD 요구사항 vs 기존 코드(As-Is) vs 계획(To-Be) 충돌 점검
- 마이그레이션 전략 없는 스택 전환 요구는 차단

충돌 시:
- 상태: `BLOCKED: STACK_CONFLICT`
- 충돌 항목/영향/결정 필요사항 문서화

## F. 구현 게이트
아래 모두 참일 때만 구현:
- TRD 상태 `READY_FOR_IMPLEMENTATION`
- Stack Contract 완결 (`<UNDECIDED>` 없음)
- Sprint 범위 명확

## G. 완료 정의 (Done)
Task 완료로 인정하려면:
- 요구사항 충족 근거가 문서화됨
- 관련 테스트 통과
- 회귀 없음
- 범위 외 변경 없음

## H. 금지사항
- 신규 앱 스캐폴딩
- PRD/Stack Contract 없는 프레임워크 도입
- 범위 외 기능 추가
- 근거 없는 “완료/안전” 선언

## I. 경로 해석 규칙 (최신 자동 선택)
- `WORK_CYCLE_ROOT`를 먼저 결정한다.
  1. **새 사이클 시작(1_AGENT_TRD부터 시작)**: `WORK_CYCLE_ROOT=./docs/improvement`로 강제
  2. `./docs/improvement`가 없으면 `./docs/improvement/{1,2,3,final,kickoff}`를 먼저 생성
  3. 진행/검증 단계에서 `./docs/improvement`가 있으면 우선 사용
  4. `./docs/improvement`가 없을 때만 `./docs/*_done` 중 최신 디렉터리 사용
- `WORK_FINAL_DIR = ${WORK_CYCLE_ROOT}/final`
- 특정 사이클명 하드코딩 금지 (예: `docs/<cycle>_done` 경로 직접 고정 금지)

## J. PRD 리비전 규칙
- 시작 기준 PRD: 최신 `PRD_REV{N}.md`
- 최종 정리 단계에서 기준 PRD를 `PRD_REV{N+1}.md`로 승격(rename)한다.
- 리네이밍 후 `README.md`, `WORKFLOW.md`, 프롬프트 참조 경로를 갱신한다.

## K. Autopilot 상태/컨텍스트 (선택)
- 자동 순차 실행(`AUTOPILOT`)을 사용할 경우, 아래 파일을 SSOT로 유지한다.
  - `${WORK_CYCLE_ROOT}/final/STATE.md`
  - `${WORK_CYCLE_ROOT}/final/CONTEXT_PACK.md`
- 대화 컨텍스트가 길어져도, 다음 단계는 위 2개 + `${WORK_CYCLE_ROOT}/final/*`만 근거로 진행한다.
