---
type: project
status: active
lane: product
repo: https://github.com/qoxmfaktmxj/vibe-hr
local_path: ~/dev/qoxmfaktmxj/vibe-hr
maturity: prototype
priority: P2
openclaw_mode: plan_only
cadence: weekly
last_reviewed: 2026-04-25
next_action: "HR 전체가 아니라 업무 cycle 단위로 완성 루프 정의"
tags: [project, saas, hr, ehr, payroll]
---

# VibeHR

## 1. 한 문장 정의

인사시스템 SaaS 후보 / 첫 번째 주요 프로젝트.

## 2. 현재 상태

- Local path: `~/dev/qoxmfaktmxj/vibe-hr`
- Branch: `main`
- HEAD: `821227b`
- Dirty: `no`

### 작동하는 것

- nested package.json: `frontend/package.json`
- found `backend/requirements.txt`
- found `backend/Dockerfile`
- found `frontend/Dockerfile`

### 미완성인 것

- 확인 필요: README/docs와 실제 실행 상태를 기준으로 별도 검증 필요.

### 위험한 것

- 확인 필요: secret, production data, deploy 설정은 이 문서화 단계에서 열람/출력하지 않음.
- OpenClaw mode: `plan_only` 기준으로만 작업.

### 다음에 닫아야 할 루프

- HR 전체가 아니라 업무 cycle 단위로 완성 루프 정의

## 3. 제품/기술 North Star

- 확인된 repo 문서와 현재 운영 목표를 바탕으로, 작고 검증 가능한 루프를 반복해 완성도를 높인다.

## 4. 이번 주 목표

- [ ] README/docs 기반 현재 상태를 한 번 더 검증한다.
- [ ] 다음 실행 큐 1개를 plan으로 닫는다.

## 5. OpenClaw 작업 큐

> OpenClaw는 이 섹션 또는 별도 `OpenClaw-Queue.md`에 있는 일만 수행한다.

- [ ] #openclaw mode:plan priority:P1 README/docs 기반 현재 상태 요약

## 6. 결정사항

| 날짜 | 결정 | 이유 | 되돌릴 조건 |
|---|---|---|---|
| 2026-04-25 | 개인 개발 운영체제 관리 대상에 등록 | 공유대화/운영 프롬프트 기준 | repo 운영 대상에서 제외될 때 |

## 7. 배운 것 / 인사이트

## 8. 관련 문서

- [[OpenClaw-Queue]]
- [[Weekly-Review]]
- [[Decisions]]

## 9. 확인된 근거

### `README.md`

Headings: # Vibe-HR, ## AI 개발 시작 전 필독 순서, ## 프로젝트 개요, ## 현재 구현 범위, ### 현재 사용 가능한 영역, ### 부분 완료 영역, ### 아직 본체가 닫히지 않은 영역, ## 기술 스택

Excerpt: # Vibe-HR ## AI 개발 시작 전 필독 순서 1. `docs/DEVELOPMENT_PRECHECK.md` 2. `AGENTS.md` 3. `config/grid-screens.json` 4. `docs/GRID_SCREEN_STANDARD.md` 5. `docs/MENU_ACTION_PERMISSION_PLAN.md` 6. 작업 대상 화면의 `page.tsx`와 실제 컴포넌트 파일

### `AGENTS.md`

Headings: # oh-my-codex - Intelligent Multi-Agent Orchestration, ## Canonical source map

Excerpt: # oh-my-codex - Intelligent Multi-Agent Orchestration You are running with oh-my-codex (OMX), a coordination layer for Codex CLI. This AGENTS.md is the top-level operating contract for the workspace. Role prompts under `prompts/*.md` are narrower execution surfaces. They must follow this file, not override it. <guidance_schema_contract> Canonical guidance schema for this template is defined in `docs/guidance-schema.md`. Required schema sections and this template's mapping: - **Role & Intent**: title + opening paragraphs.

### `CLAUDE.md`

Headings: # CLAUDE.md, ## Project, ## Source of Truth Map, ## Default Workflow, ## Risk Summary, ## Sensitive Paths

Excerpt: # CLAUDE.md > Projection document for Claude-family tools. > Canonical sources: > - `AGENTS.md` > - `docs/GOVERNANCE.md` > - `docs/ARCHITECTURE.md` > - `docs/TEST_STRATEGY.md` > - `docs/TASK_LEDGER.md`

### 문서/워크플로 후보

- `docs/AGENT_SETUP.md`
- `docs/AG_GRID_COMMON_GUIDE.md`
- `docs/AG_GRID_PERF_REMEDIATION_EXECUTION_PLAN.md`
- `docs/ARCHITECTURE.md`
- `docs/DESIGN_ICON_GUIDE.md`
- `docs/DEVELOPMENT_PRECHECK.md`
- `docs/EHR_PHASE1_EXECUTION_BACKLOG.md`
- `docs/EHR_PHASE1_INVENTORY.md`
- `docs/EHR_PHASE1_SCREEN_GAP.md`
- `docs/EHR_TABLE_RENAMING_STANDARD.md`
- `docs/EMPLOYEE_MASTER_REFACTOR_PLAN.md`
- `docs/EXECUTION_PROTOCOL.md`
- `docs/GOVERNANCE.md`
- `docs/GPT_ORCHESTRATION_SETUP.md`
- `docs/GRID_CRUD_AUDIT.md`
- `docs/GRID_SCREEN_STANDARD.md`
- `docs/HARNESS_STATUS.md`
- `docs/HR_APPOINTMENT_TABLE_DESIGN.md`
- `docs/HR_THRM_REMODEL_PLAN.md`
- `docs/MENU_ACTION_PERMISSION_PLAN.md`
- `docs/MIG-SSMS-TO-VIBE-HR.md`
- `docs/MNG-DB-TEST-PLAN.md`
- `docs/NON_SECURITY_IMPROVEMENT_PLAN.md`
- `docs/OBSERVABILITY.md`
- `docs/OMX_TEAM_GUIDE.md`
