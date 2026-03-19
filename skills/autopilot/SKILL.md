---
name: autopilot
description: This skill should be used when the user invokes "/autopilot", wants to run the pipeline, start or resume a development cycle, or says "오토파일럿 실행해줘", "pipline-kit 다음 스텝 실행", "다음 사이클 시작", "파이프라인 돌려줘", "사이클 재개", "autopilot run". Make sure to use this skill whenever pipline-kit execution or autopilot is mentioned — even if the user just says "계속 진행해줘" in the context of an ongoing cycle.
---

# Autopilot

> pipline-kit의 오토파일럿 파이프라인을 `/autopilot` 하나로 실행합니다 — 수동 복붙 없이, context/ 파일로 상태를 유지하며 PRD부터 Cleanup까지 안전하게 진행합니다.

## 커맨드 형식

```
/autopilot
/autopilot TRACK=MINOR
/autopilot TRACK=MAJOR CYCLE_LABEL=cycle-name-YYYYMMDD
/autopilot TRACK=KICKOFF
/autopilot TRACK=DESIGN CYCLE_LABEL=cycle-name-YYYYMMDD
/autopilot TRACK=BUILD
```

## 워크플로우

### Step 1: 환경 검증
**타입**: rag

Read the following files:
1. `./pipline-kit/AUTOPILOT.prompt`
2. `./pipline-kit/context/1_plan.md`
3. `./pipline-kit/context/2_context_note.md`
4. `./pipline-kit/context/3_checklist.md`

If `./pipline-kit/AUTOPILOT.prompt` does not exist:
- Output: `BLOCKED: PIPLINE_KIT_NOT_FOUND`
- Show: "pipline-kit 폴더가 없거나 submodule이 초기화되지 않았어요. `git submodule update --init --recursive` 실행 후 다시 시도해주세요."
- Stop.

If any context/ file is missing:
- Output: `BLOCKED: CONTEXT_MISSING — {파일명}`
- Show: "context/ 파일이 없어요. pipline-kit README.md를 참고하여 초기화해주세요."
- Stop.

### Step 2: 상태 파악
**타입**: prompt

Read `./docs/improvement/final/STATE.md` if it exists. If not, treat as new cycle (Phase = INIT).

Parse arguments from the command:
- `TRACK`: `KICKOFF` | `MINOR` | `MAJOR` | `DESIGN` | `BUILD` (default: `MAJOR`)
- `CYCLE_LABEL`: optional (default: `cycle-YYYYMMDD`)

Validate `TRACK` against the allowlist. If invalid, use `MAJOR` and notify the user.

Determine `current_phase` and `next_step`:
- STATE.md exists and Phase ≠ DONE → resume from `NextStep`
- STATE.md missing or Phase = DONE → start fresh

### Step 3: Phase 실행
**타입**: prompt + Agent

Spawn a subagent and pass:
- Full content of `./pipline-kit/AUTOPILOT.prompt`
- Content of all three `./pipline-kit/context/` files
- Current `TRACK`, `CYCLE_LABEL`, `current_phase`, `next_step`
- Instruction: "위 컨텍스트를 읽고 AUTOPILOT.prompt의 지침에 따라 현재 Phase를 실행하세요. 관련 pipline-kit/skills/*.md 매뉴얼을 참조하세요. 완료 후 PASS / FAIL / BLOCKED 상태와 다음 스텝을 명시하세요."

Collect: status (`PASS` / `FAIL` / `BLOCKED`) and work summary.

### Step 4: 체크포인트 확인
**타입**: review

Present the result:
```
✅ {current_phase} 완료

{작업 요약 2-3줄}

→ 다음: {next_phase}
계속 진행할까요?
```

If status = `BLOCKED`:
- Show `StopReason` and `NextStep` clearly.
- Save state and stop — do not auto-proceed.

If user declines to continue: save state and stop cleanly.

### Step 5: context/ 동기화
**타입**: generate

Update `./docs/improvement/final/STATE.md`:
- Phase: {next_phase}
- Current Sprint: {N if applicable}
- Attempts updated
- NextStep: what to do on next `/autopilot` run

Update `./docs/improvement/final/CONTEXT_PACK.md` (keep under 400 lines):
- Cycle Label, Track, current Phase, recent errors, NextStep

Output:
```
🔄 상태 저장 완료
현재: {phase} → 다음: {next_phase}
다시 실행: /autopilot TRACK={TRACK}
```

## Settings

| 설정 | 기본값 | 변경 방법 |
|------|--------|-----------|
| TRACK | `MAJOR` | `/autopilot TRACK=MINOR` |
| CYCLE_LABEL | `cycle-YYYYMMDD` | `/autopilot CYCLE_LABEL=my-label` |
| MAX_SPRINTS_PER_RUN | 4 | `./pipline-kit/AUTOPILOT.prompt` 내 값 수정 |
| MAX_QA_CYCLES_PER_SPRINT | 3 | `./pipline-kit/AUTOPILOT.prompt` 내 값 수정 |

## 자주 쓰는 패턴

| 상황 | 명령어 |
|------|--------|
| 신규 대형 기능 (Claude 혼자) | `/autopilot TRACK=MAJOR CYCLE_LABEL=cycle-feature-YYYYMMDD` |
| 작은 버그 수정 | `/autopilot TRACK=MINOR` |
| 중단된 사이클 재개 | `/autopilot` (STATE.md 자동 읽기) |
| 새 프로젝트 시작 | `/autopilot TRACK=KICKOFF` |
| Codex 병렬 투입 — 설계 단계 | `/autopilot TRACK=DESIGN CYCLE_LABEL=cycle-feature-YYYYMMDD` |
| Codex 병렬 투입 — 구현 단계 | `/autopilot TRACK=BUILD` (DESIGN 완료 후) |

## PUMASI 흐름

```
1. /autopilot TRACK=DESIGN   → Claude가 설계 완료 (TRD→BACKLOG)
                                     "BACKLOG 확정. Codex 투입 준비됨" 메시지 출력
2. (BACKLOG 검토 후)
3. /autopilot TRACK=BUILD  → 각 Sprint Task를 Agent 병렬 투입
                                     결과 통합 → QA → Cleanup
```

## References
- **`../../AUTOPILOT.prompt`** — 오토파일럿 메인 로직 (상태 머신 전체)
- **`../../context/`** — 외부 기억 장치 (1_plan, 2_context_note, 3_checklist)
- **`../`** — Phase별 실행 매뉴얼 (prd_builder, implement_sprint, sprint_qa 등)
