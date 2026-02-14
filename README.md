# Pipeline Kit (pipline-kit)

기존 코드베이스 개선(Enhancement)을 **안전하게 반복**하기 위한 프롬프트 세트.

## 빠른 시작
- 이 레포는 **범용**이다. 어떤 프로젝트든 가져다 써도 된다.
- 사용 시 권장 규칙: 프로젝트 루트에 폴더명을 **항상** `pipline-kit/`로 둔다.
  - (프롬프트들이 `./pipline-kit/...` 경로를 기준으로 참조함)
- 추천 엔트리포인트: `AUTOPILOT.prompt`

### 설치 방법(프로젝트별)
아래 중 하나를 선택:
1) Git submodule (팀/재현성에 가장 좋음)
```bash
git submodule add <REPO_URL> pipline-kit
git submodule update --init --recursive
```
2) 단순 클론 + 메인 레포에서 무시(개인 로컬용)
```bash
git clone <REPO_URL> pipline-kit
```
메인 프로젝트의 `.gitignore`에 `pipline-kit/`를 추가하면 커밋에 섞이지 않는다.

## 트랙 (3)
1. `KICKOFF`
- 프로젝트 시작(그린필드) 1회용: 스택/구조 결정 + 최소 스캐폴딩 + 실행/테스트 스모크까지.
2. `MINOR`
- 작은 개선/버그 수정: 문서 최소화 + 게이트 완화(단, PRD/Stack Contract는 유지).
3. `MAJOR`
- 큰 개선/리스크 높은 변경: 풀 문서 + 하드 게이트 + 스프린트 반복 루프.

## 경로 규칙 (범용)
- `WORK_CYCLE_ROOT`를 먼저 결정한다.
  - 새 사이클 시작(1번 프롬프트) 시: `./docs/improvement` 강제
  - `./docs/improvement`가 없으면 `./docs/improvement/{1,2,3,final,kickoff}` 자동 생성
  - 진행/검증 단계는 `./docs/improvement` 우선
  - 없으면: `./docs/*_done` 중 최신 디렉터리
- 산출물 경로는 항상 `${WORK_CYCLE_ROOT}` 기준으로 사용한다.
  - `${WORK_CYCLE_ROOT}/1/*`
  - `${WORK_CYCLE_ROOT}/2/*`
  - `${WORK_CYCLE_ROOT}/3/*`
  - `${WORK_CYCLE_ROOT}/final/*`
- 특정 사이클명 하드코딩 금지 (예: `docs/<cycle>_done` 형태를 직접 고정하지 않음)

## 권장 순서

### AUTOPILOT (단일 실행)
0. `AUTOPILOT.prompt`

### KICKOFF (프로젝트 시작)
0. `0_KICKOFF_CONCERNS.md`
1. `KICKOFF_PROJECT.prompt`

### MINOR (작은 개선)
0. `0_PROCESS_CONCERNS.md` (필독 규칙)
1. `1_AGENT_TRD.prompt`
2. `FINAL_MERGE.prompt` (MINOR는 `2/`, `3/` 누락 허용)
3. `IMPLEMENT_SPRINT.prompt` (Sprint 번호 입력)
4. `SPRINT_QA.prompt` (Sprint 번호 입력)
5. `FINAL_CLEANUP_CONFIRM.prompt`

### MAJOR (큰 개선)
0. `0_PROCESS_CONCERNS.md` (필독 규칙)
1. `1_AGENT_TRD.prompt`
2. `2_AGENT_API.prompt`
3. `3_AGENT_PLAN.prompt` (예비 백로그 포함)
4. `FINAL_MERGE.prompt`
5. `FINAL_BACKLOG.prompt` (예비→확정)
6. Sprint 반복:
   - `IMPLEMENT_SPRINT.prompt` (Sprint 번호 입력)
   - `SPRINT_QA.prompt` (Sprint 번호 입력)
7. `FINAL_QA_RELEASE.prompt` (전체 Sprint 종료 후 1회)
8. `FINAL_CLEANUP_CONFIRM.prompt` (최종 정리/다음 액션 확정 + PRD `REV` 승격 + 폴더명 정리)
