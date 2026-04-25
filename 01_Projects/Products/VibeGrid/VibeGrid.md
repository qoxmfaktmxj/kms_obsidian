---
type: project
status: active
lane: product
repo: https://github.com/qoxmfaktmxj/vibe-grid
local_path: ~/dev/qoxmfaktmxj/vibe-grid
maturity: prototype
priority: P1
openclaw_mode: branch_pr
cadence: weekly
last_reviewed: 2026-04-25
next_action: "Public API, 테스트, clipboard/excel/persistence 품질을 우선 안정화"
tags: [project, saas, grid, frontend, platform]
---

# VibeGrid

## 1. 한 문장 정의

업무형 그리드 제품 / Vibe 계열 공통 자산.

## 2. 현재 상태

- Local path: `~/dev/qoxmfaktmxj/vibe-grid`
- Branch: `master`
- HEAD: `4dc2359`
- Dirty: `no`

### 작동하는 것

- package name: `vibe-grid`
- npm scripts: build, build:bench, build:playground, ci, dev, dev:bench, dev:playground, lint, lint:bench, lint:packages, lint:playground, start, test:core, test:e2e, test:e2e:local, test:e2e:smoke
- devDependencies: `@playwright/test`, `@types/node`, `@types/react`, `@types/react-dom`, `eslint`, `eslint-config-next`, `typescript`

### 미완성인 것

- 확인 필요: README/docs와 실제 실행 상태를 기준으로 별도 검증 필요.

### 위험한 것

- 확인 필요: secret, production data, deploy 설정은 이 문서화 단계에서 열람/출력하지 않음.
- OpenClaw mode: `branch_pr` 기준으로만 작업.

### 다음에 닫아야 할 루프

- Public API, 테스트, clipboard/excel/persistence 품질을 우선 안정화

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

Headings: # VibeGrid, ## 목적, ## 워크스페이스 구성, ### 앱, ### 패키지, ## 시작하기, ### 설계 참조 문서, ## 로컬 개발

Excerpt: # VibeGrid VibeGrid는 EHR 관련 애플리케이션에서 IBSheet 스타일 비즈니스 그리드를 대체하기 위한 독립형 내부 그리드 제품 워크스페이스입니다. --- ## 목적 - 페이지 레벨 테이블 위젯이 아닌, 재사용 가능한 비즈니스 그리드 제품 구축 - `TanStack Table`은 내부 엔진 구현 상세로만 유지 — 앱에 노출 금지 - `row-first` HR 워크플로우를 위한 안정적인 앱 대면 API 제공 - `EHR_6` 및 `vibe-hr`로의 본격 마이그레이션 전에 IBSheet 대체 동작 검증

### `AGENTS.md`

Headings: # VibeGrid Working Rules, ## 1. Read Order Before Touching Code, ## 2. What Has Already Been Built, ### Completed foundation and behavior slices, ### What exists right now, ### Cu

Excerpt: # VibeGrid Working Rules This repository is a shared grid product workspace. It is not a one-off demo and it is not a page-level table wrapper. The project exists to build an IBSheet-replacement business grid that can be consumed by multiple apps such as `EHR_6` and later `vibe-hr`. ## 1. Read Order Before Touching Code Read these files in order before making changes: 1. `README.md` 2. `CHANGELOG.md`

### `CHANGELOG.md`

Headings: # Changelog, ## Unreleased, ### Added, ### Fixed, ### Changed

Excerpt: # Changelog All meaningful changes to the shared VibeGrid product should be recorded here. ## Unreleased ### Added - Shared density option on `VibeGrid` with `compact`, `default`, and `comfortable` modes, plus density comparison controls in Grid Lab and Bench. - Real-grid performance verification with actual `VibeGrid` render-path coverage. - Stable vs experimental boundary documentation. - Hub smoke regression coverage.

### 문서/워크플로 후보

- `docs/AGENTS.md`
- `docs/adr/0001-product-scope.md`
- `docs/compatibility/README.md`
- `docs/compatibility/ibsheet8-feature-matrix.md`
- `docs/deployment/vercel-github-deploy.md`
- `docs/design/AGENTS.md`
- `docs/design/design-performance-guardrails.md`
- `docs/design/stitch-design-translation.md`
- `docs/development/AGENTS.md`
- `docs/development/style-change-bench-checklist.md`
- `docs/development/vibe-grid-ai-consumption-guide.md`
- `docs/development/vibe-grid-development-guide.md`
- `docs/release/AGENTS.md`
- `docs/release/public-api-stability.md`
- `docs/release/release-routine.md`
- `docs/roadmap/AGENTS.md`
- `docs/roadmap/README.md`
- `docs/roadmap/bench-mode-split-design.md`
- `docs/roadmap/current-execution-plan.md`
- `docs/roadmap/feature-expansion-backlog.md`
- `docs/roadmap/p5-performance-status.md`
- `docs/roadmap/p6-product-infrastructure-status.md`
- `docs/roadmap/p7-test-release-status.md`
- `docs/roadmap/slice-1-status.md`
- `docs/roadmap/slice-2-status.md`
