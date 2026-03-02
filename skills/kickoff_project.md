# 스킬: Kickoff Project (프로젝트 시작 / 그린필드)

> **역할:** 프로젝트 Kickoff 담당
> **선행 조건:** 반드시 `skills/0_kickoff_concerns.md`를 먼저 읽는다.

## 🎯 목표
- PRD 기반으로 "작동하는 최소 골격(MVP skeleton)"을 만든다.
- 과도한 설계/과도한 폴더/과도한 스택 도입 없이, 실행/테스트까지 연결한다.

## 📥 입력
- PRD (없으면 진행 금지)
- 사용자 제약(선호 언어/프레임워크, 배포 형태, 금지 스택 등)
- (선택) 기존 레포가 이미 존재한다면 그 구조(단, 이 트랙은 그린필드도 허용)

## 📤 출력
- 코드 스캐폴딩 (필요한 최소 파일/폴더/설정)
- `README.md` (설치/실행/테스트 명령 포함)
- `${WORK_CYCLE_ROOT}/kickoff/KICKOFF.md` (결정/근거/검증 결과 기록)

## 🚨 하드 게이트
1. **PRD 확인**
   - PRD가 없으면 상태: `BLOCKED: PRD_REQUIRED` + 필요한 질문만 출력
2. **스택 결정**
   - 스택이 미결정이면 상태: `BLOCKED: STACK_DECISION_REQUIRED`
   - 임의 선택 금지(후보 1개 제안 + 사용자 승인)

## 🔧 작업 절차
1. PRD 요약 (목표/범위/비기능/제약)
2. Stack Contract 작성
   - 결정값 + 출처(PRD 또는 사용자 승인) 명시
3. 최소 구조 설계
   - 디렉터리 트리(최소) 제안
   - **도메인 주도 설계(DDD) 패턴 적용:** 비즈니스 용어와 폴더명을 일치시켜 AI가 읽어야 할 파일 범위를 좁힌다.
4. 스캐폴딩 구현
   - 실제로 실행 가능한 최소 엔트리포인트(서버/CLI 등) 생성
   - 최소 테스트 1개 이상 추가
5. 검증
   - 설치/실행/테스트 명령을 실제로 실행하고 결과를 기록

## 📋 KICKOFF.md 필수 항목
- Status (DONE / BLOCKED:*)
- 목표/범위 (In/Out)
- Stack Contract (결정값 + 출처)
- 생성된 구조 요약(트리)
- 실행 방법 / 테스트 방법
- 검증 결과(성공/실패 + 로그 요약)
- 다음 단계 추천: `MINOR` 또는 `MAJOR` 트랙으로 넘어가기 위한 조건

## WORK_CYCLE_ROOT 규칙
- 기본값: `./docs/improvement`
- 없으면 `./docs/improvement/{1,2,3,final,kickoff}` 생성

## 🔗 하니스 연동 (랄프 루프 사용 시)
- 완료 후 `context/3_checklist.md`의 KICKOFF 항목을 `[x]`로 마킹
- `context/1_plan.md`에 Stack Contract 및 생성된 구조 요약 반영
