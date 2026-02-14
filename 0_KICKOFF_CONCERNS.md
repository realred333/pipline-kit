# 0. 필독 규칙 (KICKOFF 전용)

이 문서는 **프로젝트 시작(그린필드)** 트랙의 최상위 규칙이다.
기존 개선(Enhancement) 트랙에서는 이 문서를 쓰지 말고 `0_PROCESS_CONCERNS.md`를 사용한다.

## A. 작업 타입 고정
- 기본값은 `프로젝트 시작(KICKOFF)`이다.
- PRD 없이 “일단 만들어두고 보자” 식의 스캐폴딩 금지.

## B. 컨텍스트 게이트
아래가 없으면 진행 금지:
- PRD (없으면 상태: `BLOCKED: PRD_REQUIRED`)
- 타겟 형태 (예: Web / API / CLI / Library 중 최소 1개 명시)

## C. 스택 결정 게이트
아래 항목은 `결정값 + 출처(PRD 또는 사용자 승인)`가 필수:
- 언어/런타임
- 실행 모델(웹 프레임워크/CLI 등)
- 테스트 도구
- 패키지/빌드 도구

미결정 처리:
- PRD 명시값 우선
- PRD 미명시 시: 후보 1개만 제안하고 사용자 승인 요청
- 승인 없이는 `BLOCKED: STACK_DECISION_REQUIRED`

## D. 최소 스캐폴딩 원칙
- 목표는 “작동하는 최소 골격(MVP skeleton)”이다.
- PRD에 없는 인증/결제/대규모 인프라/복잡한 아키텍처 도입 금지.
- 첫 커밋 기준으로 아래를 만족해야 한다:
  - 실행 방법이 문서화됨
  - 최소 1개의 스모크 테스트(또는 단위 테스트) 존재
  - 기본 디렉터리 구조가 명확함

## E. 완료 정의 (Done)
아래가 모두 참일 때만 Kickoff 완료로 인정:
- `README.md`에 설치/실행/테스트 명령이 명시됨
- 최소 실행(서버 기동 또는 CLI 실행)이 실제로 동작함
- 테스트가 실행되고 통과함

## F. 경로 규칙
- `WORK_CYCLE_ROOT` 기본값: `./docs/improvement`
- `./docs/improvement`가 없으면 `./docs/improvement/{1,2,3,final,kickoff}`를 생성한다.
- Kickoff 산출물 루트: `${WORK_CYCLE_ROOT}/kickoff`
