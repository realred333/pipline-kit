# 2. 현재 맥락 및 변수 노트 (Context Note)

> **💡 AI 에이전트 행동 지침:**
> 너의 뇌(기억)는 매 루프마다 포맷된다.
> 따라서 코딩 중 고민했던 흔적, 미처 해결 못한 오류 트레이스, 다음 단계에서 필요한 변수 상태 등 **'휘발되면 안 되는 모든 맥락'**을 여기에 꼼꼼히 기록하고 종료해.
> 다음 루프의 AI는 이 문서만 보고 맥락을 복원한다.

## 현재 Phase
- **Track:** (KICKOFF / MINOR / MAJOR)
- **Phase:** (PRD → TRD → API → PLAN → MERGE → BACKLOG → SPRINT_IMPLEMENT → SPRINT_QA → FINAL_QA → CLEANUP → DONE)
- **Current Sprint:** N
- **최근 작업 요약:** (방금 전 루프까지 무엇을 만들고 있었는지 간략히 요약)

## 오픈 이슈 / 다음 루프 해결 과제
- (에러가 발생해서 해결 중이라면 에러 로그의 핵심과 시도한 해결책을 적어)
- (다음 루프의 AI에게 알려줘야 할 중요한 변수 상태값이나 제약조건)

## 핵심 결정 로그
| 루프 # | 결정사항 | 근거 |
|---|---|---|
| 1 | (예: React 대신 Vue 사용) | (예: 기존 코드가 Vue 기반) |

## 전역 변수 / 핵심 레퍼런스
- `WORK_CYCLE_ROOT`: `./docs/improvement`
- `CYCLE_LABEL`: (미정)
- (기타 잊지 말아야 할 전역 설정이나 주의사항)
