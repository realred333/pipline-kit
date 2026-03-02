# 🚀 Pipeline Kit (pipline-kit) — 하니스 오토파일럿 시스템

단순한 프롬프트 묶음이 아닌, **AI가 24시간 자율적으로 에러 없이 동작할 수 있는 '하니스(Harness) 기반 오토파일럿 시스템'**입니다.

대화가 길어지면 AI가 지시를 잊거나 환각을 일으키는 **'멍청한 영역(Dumb Zone)'** 문제를 해결하고, 100배 안정적인 코딩 루프를 만드는 것이 목표입니다.

---

## 💡 핵심 개념: 랄프 위검 루프 (Ralph Wiggum Loop)

AI와 대화가 길어지면 앞의 지시를 잊고 엉뚱한 코드를 짜기 시작합니다. 이를 해결하기 위해:

1. **AI가 한 작업을 마치면, 기존 대화를 완전히 지우고 깨끗한 상태로 재시작**합니다.
2. **AI의 기억을 파일(`context/` 폴더)에 저장**하여, 새로 깨어난 AI가 이 파일만 읽고 즉시 다음 작업을 이어갑니다.
3. 매번 최고 성능의 맑은 정신으로 작업하므로 **환각 없이 끝까지 완주**합니다.

비유: 요리사에게 레시피 카드를 쥐여주고 "이거 다 만들면 다음 카드 봐"라고 시킨 뒤 퇴근하는 것과 같습니다.

---

## 📁 폴더 구조

```
pipline-kit/
├── 0_AGENT_SYSTEM_PROMPT.md   # AI 에이전트의 페르소나 및 행동 원칙
├── AUTOPILOT_LOOP.sh          # 랄프 위검 루프 실행 스크립트
├── README.md                  # 이 파일
│
├── context/                   # ★ 외부 기억 장치 (AI의 뇌 대신 사용)
│   ├── 1_plan.md              # 전체 계획 및 목표 (나침반)
│   ├── 2_context_note.md      # 이전 루프의 맥락, 에러, 결정사항 (단기 기억)
│   └── 3_checklist.md         # 해야 할 일 목록 (작업 큐)
│
├── hooks/                     # 자동 제어 훅 (품질 게이트)
│   ├── pre_hook.md            # 작업 시작 전 강제 체크리스트
│   ├── post_hook.md           # 작업 완료 후 강제 자가 점검
│   ├── pre_run_domain_check.md  # SDD/DDD 강제 숙지 선언문
│   └── post_run_self_check.md   # 에러/보안 셀프 체크
│
├── skills/                    # 전문 스킬 매뉴얼 (기존 .prompt 파일의 진화형)
│   ├── 0_process_concerns.md  # 필독 규칙 (Enhancement: MINOR/MAJOR)
│   ├── 0_kickoff_concerns.md  # 필독 규칙 (KICKOFF)
│   ├── prd_builder.md         # PRD 작성 (스펙 주도 개발)
│   ├── agent_trd.md           # TRD / 아키텍처 설계
│   ├── agent_api.md           # API / 데이터 모델 설계
│   ├── agent_plan.md          # 실행 계획 / 백로그 초안
│   ├── kickoff_project.md     # 프로젝트 시작 (그린필드)
│   ├── implement_sprint.md    # 스프린트 구현
│   ├── sprint_qa.md           # 스프린트 QA
│   ├── final_merge.md         # 문서 통합
│   ├── final_backlog.md       # 백로그 확정
│   ├── final_qa_release.md    # 최종 QA / 릴리즈 판정
│   ├── final_cleanup.md       # 최종 정리 / 마감
│   └── domain_rules.md        # 도메인 주도 설계(DDD) 규칙
│
├── docs/                      # 작업 산출물 저장소
│
└── (기존 .prompt 파일들)      # 레거시 — skills/ 폴더로 모두 마이그레이션 완료
```

---

## 🎮 사용 방법

### 방법 1: 수동 복붙 모드 (클로드 웹, 제미나이 웹, Cursor IDE 등) ✅ 추천

가장 직관적인 방법입니다. 터미널에서 스크립트를 켜고, AI에게 프롬프트를 복붙합니다.

#### 사전 준비
1. `context/3_checklist.md`를 열어서 님의 프로젝트에 맞게 내용을 수정합니다.
   - 어떤 순서로 무엇을 만들 것인지 체크리스트를 세팅합니다.
   - 기본값은 전체 파이프라인(PRD → TRD → API → PLAN → Sprint → QA → Cleanup) 순서입니다.
2. `context/1_plan.md`를 열어서 님의 프로젝트 목표를 간략히 적습니다.

#### 실행 (매 루프)
```bash
# 1) 터미널에서 스크립트 실행
bash AUTOPILOT_LOOP.sh

# 2) .temp_prompt.txt가 생성됩니다.
#    VS Code에서 열거나, cat으로 내용을 확인합니다.
cat .temp_prompt.txt

# 3) 내용 전체를 복사 (Ctrl+A → Ctrl+C)

# 4) 클로드/제미나이/Cursor 채팅창에 붙여넣기 (Ctrl+V)

# 5) AI가 다음과 같이 동작합니다:
#    - 외부 기억 장치(context/)를 읽고 현재 상태를 파악
#    - 체크리스트에서 첫 번째 [ ] 항목을 찾아 작업 수행
#    - 관련 스킬(skills/*.md) 매뉴얼을 참조하여 고품질 결과물 생성
#    - 에러/보안 셀프 체크 후 context/ 파일들을 업데이트
#    - "LOOP_DONE" 선언

# 6) 터미널로 돌아와 '엔터' 누르기 → 다음 루프 시작!
```

#### 반복
위 3~6단계를 체크리스트의 모든 항목이 `[x]`가 될 때까지 반복합니다. 매번 AI는 맑은 정신으로 깨어나서 이전 맥락을 파일로부터 완벽히 복원합니다.

---

### 방법 2: 완전 자동 모드 (Aider, Claude Code 등 CLI 도구)

`AUTOPILOT_LOOP.sh`의 주석 처리된 부분을 해제하면, 복붙 없이 **밤새도록 100% 자동**으로 돌릴 수 있습니다.

```bash
# AUTOPILOT_LOOP.sh 안의 이 부분을 찾아서 주석 해제:
aider --message-file "$TEMP_PROMPT"
```

이후 `bash AUTOPILOT_LOOP.sh`만 실행하면 스크립트가 프롬프트 생성 → AI 호출 → 결과 반영을 자동 반복합니다.

---

### 방법 3: 기존 AUTOPILOT.prompt 방식 (레거시)

기존처럼 `AUTOPILOT.prompt`를 한 번에 AI에게 던져서 순차 실행시키는 방식도 여전히 가능합니다. 다만, 대화가 길어지면 AI의 성능이 저하될 수 있습니다.

---

## ⚙️ 내 프로젝트에 적용하는 법

### 설치
```bash
# Git submodule (팀/재현성에 가장 좋음)
git submodule add <REPO_URL> pipline-kit
git submodule update --init --recursive

# 또는 단순 클론 (개인 로컬용)
git clone <REPO_URL> pipline-kit
# 메인 프로젝트의 .gitignore에 pipline-kit/ 추가
```

### 초기 세팅
1. `context/1_plan.md` — 님의 프로젝트 목표와 스택을 적기
2. `context/3_checklist.md` — 해야 할 일을 순서대로 적기
3. `skills/domain_rules.md` — (선택) 님의 도메인 용어 사전 적기
4. `bash AUTOPILOT_LOOP.sh` 실행!

---

## 🏗 트랙 (Track) 시스템

| 트랙 | 용도 | 문서 수준 |
|---|---|---|
| `KICKOFF` | 프로젝트 신규 시작 (그린필드) | 최소 스캐폴딩 + 스모크 테스트 |
| `MINOR` | 작은 개선/버그 수정 | 문서 최소화, 게이트 완화 |
| `MAJOR` | 큰 개선/리스크 높은 변경 | 풀 문서 + 하드 게이트 + 스프린트 반복 |

---

## 🔄 전체 파이프라인 순서 (MAJOR 기준)

```
PRD 작성 → TRD/아키텍처 → API/데이터모델 → 실행계획/백로그초안
    → 문서통합(Merge) → 백로그확정
    → [Sprint 루프: 구현 → QA → 구현 → QA ...]
    → 최종 QA/릴리즈 → Cleanup/마감
```

각 단계마다 AI는 해당 `skills/*.md` 매뉴얼을 읽고 그 지침에 따릅니다.

---

## 🧠 5가지 하니스 엔지니어링 핵심 원칙

1. **스킬(Skills) 기반 매뉴얼화** — `.prompt` 파일들을 AI가 참조하는 전문 마크다운 매뉴얼로 변환
2. **랄프 위검 루프 & 외부 기억 장치** — 대화 초기화 + `context/` 3개 문서로 기억 유지
3. **훅(Hook)을 통한 자동 제어** — 시작 전/완료 후 강제 체크(SDD/DDD/보안)
4. **스펙 주도 개발(SDD) 강제** — 코딩 전 반드시 PRD(주문서) 작성
5. **도메인 주도 설계(DDD) 패턴** — 비즈니스 용어 = 코드 용어, 환각 방지
