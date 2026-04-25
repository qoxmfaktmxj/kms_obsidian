---
type: project
status: active
lane: product
repo: https://github.com/qoxmfaktmxj/tripcart
local_path: ~/dev/qoxmfaktmxj/tripcart
maturity: idea
priority: P3
openclaw_mode: branch_pr
cadence: paused
last_reviewed: 2026-04-25
next_action: "개인 실험 프로젝트로 보존하되 당장은 낮은 우선순위"
tags: [project, travel, personal, saas]
---

# TripCart

## 1. 한 문장 정의

개인 여행/카트형 실험 프로젝트.

## 2. 현재 상태

- Local path: `~/dev/qoxmfaktmxj/tripcart`
- Branch: `main`
- HEAD: `eaa9c7b`
- Dirty: `no`

### 작동하는 것

- package name: `tripcart`
- npm scripts: build, clean, dev, format, lint, test, typecheck
- devDependencies: `prettier`, `turbo`, `typescript`
- found `pnpm-workspace.yaml`

### 미완성인 것

- 확인 필요: README/docs와 실제 실행 상태를 기준으로 별도 검증 필요.

### 위험한 것

- 확인 필요: secret, production data, deploy 설정은 이 문서화 단계에서 열람/출력하지 않음.
- OpenClaw mode: `branch_pr` 기준으로만 작업.

### 다음에 닫아야 할 루프

- 개인 실험 프로젝트로 보존하되 당장은 낮은 우선순위

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

Headings: ## What it is, ## Current status, ### Product interaction model, ## Change log, ### 2026-04-15, ### 2026-04-09, ### Verified state (2026-04-15)

Excerpt: ﻿# TripCart TripCart는 여행 장소를 장바구니처럼 담고, 실행 가능한 일정으로 정리하는 guest-first 여행 계획 제품입니다. The product principle is simple: planning and execution are not the same thing. ## What it is - 여행 장소 후보를 먼저 모읍니다. - 저장한 후보를 초안 플랜으로 정리합니다. - 필요할 때 로그인해 브라우저에 담아둔 데이터를 계정으로 이어서 관리합니다. ## Current status

### `AGENTS.md`

Headings: # AGENTS.md — TripCart (Codex 실행 진입점), ## 0. 읽기 순서, ## 1. Source of Truth, ## 2. 위험도와 자율성 (GOVERNANCE.md §4~§7), ### R3 민감 경로, ## 3. 핵심 제품 원칙, ## 4. 기술 원칙, ## 5. 구현 순서 규칙

Excerpt: # AGENTS.md — TripCart (Codex 실행 진입점) 이 파일은 canonical docs의 **projection**이다. 정본은 `docs/` 폴더다. Codex의 역할은 **구현/수정/테스트**다. 분석/리뷰는 Claude가 한다. ## 0. 읽기 순서 작업 시작 전에 반드시 아래 순서로 읽는다. 1. `docs/00_READ_THIS_FIRST.md` 2. `docs/PRODUCT_MASTER_PLAN.md` 3. `docs/ARCHITECTURE.md`

### `CLAUDE.md`

Headings: # CLAUDE.md — TripCart (Claude 분석 진입점), ## 현재 상태 (2026-04-15), ## Phase 2 진입 전 필수 TODO, ## 구현된 API Endpoints (Phase 1 implemented slice), # Auth, # Places (public read), # Saved Places (인증 필수), # Plans (인증 필수)

Excerpt: # CLAUDE.md — TripCart (Claude 분석 진입점) 이 파일은 canonical docs의 **projection**이다. 정본은 `docs/` 폴더다. Claude의 역할은 **분석/설계/리뷰**다. 구현은 Codex 또는 executor 에이전트가 한다. ## 현재 상태 (2026-04-15) ``` Phase 0: 완료 — monorepo scaffolding, pnpm, Supabase init, canonical schema migration Phase 1: 구현됨; audit hardening pending — Auth, Places, Saved Places, Plans CRUD, Plan Stops Phase 1.5: 구현됨; QA/docs alignment pending — guest-first trial, public landing, login migration, mobile tab nav

### `CHANGELOG.md`

Headings: # CHANGELOG, ## [0.0.2.0] - 2026-04-10, ### Added, ### Changed, ### Fixed, ### Verified, ## [0.0.1.9] - 2026-04-09, ### Changed

Excerpt: # CHANGELOG All notable changes to this project will be documented in this file. ## [0.0.2.0] - 2026-04-10 ### Added - Added shared home-view and auth-form helpers so the refreshed guest landing and auth flows keep one source of truth for card formatting, category routing, and validation messaging. ### Changed - Refreshed the guest-first `/`, `/places`, `/saved-places`, `/plans`, and `/plans/[id]` surfaces so home categories route into live filters, guest trip cards show real start times, and saved-place and plan screens read cleanly on both desktop and mobile. - Updated the guest-first Playwright flow to match the new landing, place save, draft plan creation, and guest migration UI.

### 문서/워크플로 후보

- `docs/00_READ_THIS_FIRST.md`
- `docs/API_CONTRACT_v0.2.md`
- `docs/ARCHITECTURE.md`
- `docs/DESIGN_SYSTEM.md`
- `docs/DEVELOPMENT_OPERATING_SYSTEM.md`
- `docs/EXECUTION_PROTOCOL.md`
- `docs/GOVERNANCE.md`
- `docs/PRODUCT_MASTER_PLAN.md`
- `docs/ROADMAP.md`
- `docs/SECURITY.md`
- `docs/TEST_STRATEGY.md`
- `docs/evals/TASK_LEDGER.md`
- `docs/tripcart-design-tokens.final.ts`
- `docs/tripcart_schema_canonical_v0.3.sql`
- `docs/tripcart_schema_v0.2_hardening_patch.sql`
- `.github/workflows/ci.yml`
