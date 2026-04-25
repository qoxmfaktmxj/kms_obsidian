---
type: project
status: active
lane: work
repo: https://github.com/qoxmfaktmxj/jarvis
local_path: ~/dev/qoxmfaktmxj/jarvis
maturity: prototype
priority: P0
openclaw_mode: plan_only
cadence: daily
last_reviewed: 2026-04-25
next_action: "다음 주 sprint 목표를 LLM Wiki ingest/query/lint 중 하나의 닫힌 루프로 정의"
tags: [project, work, llm-wiki, jarvis]
---

# Jarvis

## 1. 한 문장 정의

LLM Wiki 엔진 후보 / 업무 지식 시스템 실험.

## 2. 현재 상태

- Local path: `~/dev/qoxmfaktmxj/jarvis`
- Branch: `main`
- HEAD: `0648e43`
- Dirty: `no`

### 작동하는 것

- package name: `jarvis`
- npm scripts: audit:rsc, build, db:generate, db:migrate, db:push, db:seed, db:studio, dev, eval:budget-test, eval:run, lint, test, test:integration, type-check, wiki:check
- dependencies: `oracledb`, `pg`
- devDependencies: `@types/node`, `@types/pg`, `dotenv`, `openai`, `tsx`, `turbo`, `typescript`, `xlsx`
- found `pnpm-workspace.yaml`

### 미완성인 것

- 확인 필요: README/docs와 실제 실행 상태를 기준으로 별도 검증 필요.

### 위험한 것

- 확인 필요: secret, production data, deploy 설정은 이 문서화 단계에서 열람/출력하지 않음.
- OpenClaw mode: `plan_only` 기준으로만 작업.

### 다음에 닫아야 할 루프

- 다음 주 sprint 목표를 LLM Wiki ingest/query/lint 중 하나의 닫힌 루프로 정의

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

Headings: # Jarvis, ## 1. 이 프로젝트가 해결하려는 문제, ## 2. Karpathy LLM Wiki 방식 — 왜 RAG가 아닌가, ## 3. 핵심 아키텍처 — 3-레이어 모델

Excerpt: # Jarvis **LLM이 raw 자료를 읽어 사내 위키를 컴파일하고, 사용자는 compiled wiki를 탐색하는 엔터프라이즈 지식 시스템.** Jarvis는 검색 포털이 아닙니다. [Karpathy의 LLM Wiki 구상](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)을 엔터프라이즈 멀티테넌트 환경(5000명 규모)으로 확장한 **지식 컴파일·북키핑 자동화 플랫폼**입니다. 원문 업로드·검색·청크 임베딩은 수단일 뿐이고, 제품의 본체는 **LLM이 지속 편집하는 영속 위키**입니다. > **2026-04-15 피벗.** "6-레인 RAG 포털"에서 "LLM Wiki 컴파일 시스템"으로 정체성을 재정의했습니다. 구 README는 [`docs/_archive/2026-04-pivot/README.rag-era.md`](docs/_archive/2026-04-pivot/README.rag-era.md)에 보존되어 있습니다. 최상위 스키마·워크플로 규약은 [`WIKI-AGENTS.md`](WIKI-AGENTS.md)를 먼저 참고하세요. --- ## 1. 이 프로젝트가 해결하려는 문제 사내 지식 시스템이 계속 실패하는 원인은 **검색의 약점**이 아니라 **지식의 휘발과 파편화**입니다. - 사람들이 질문하고 답을 얻지만, 그 답이 **어디에도 축적되지 않습니다**. 다음 사람이 같은 질문을 반복합니다.

### `AGENTS.md`

Headings: # Jarvis — Agent Instructions, ## 프로젝트 개요, ## 개발 명령어, ## 하네스: 방법론은 superpowers, 도메인은 Jarvis 스킬, ### Codex CLI에서도 superpowers 사용, # Codex CLI 내에서, # 목록에서 superpowers를 찾아 Install Plugin, ### 방법론 위임 매핑

Excerpt: # Jarvis — Agent Instructions > 이 파일은 Codex CLI, Claude Code, 그리고 이 프로젝트에서 일하는 모든 AI 에이전트를 위한 최상위 지시문입니다. > Claude Code 사용자라면 `CLAUDE.md`가 자동 로드되지만, **이 파일도 같은 원칙을 담고 있으니 충돌 시 양쪽을 모두 참조**하세요. > Codex CLI 사용자라면 이 파일이 일차 진입점입니다. ## 프로젝트 개요 Jarvis = **사내 업무 시스템 + LLM 컴파일 위키**를 하나의 TypeScript 모노레포로 통합한 엔터프라이즈 지식 플랫폼. 2026-04-15부터 Karpathy LLM Wiki 방식 + Graphify 구조보조 + Git 단일 진실원천으로 피벗 중. 상세는 `WIKI-AGENTS.md` 참조. Next.js 15 App Router + Drizzle + PostgreSQL 16 (+pg_trgm, unaccent; pgvector는 레거시 호환용 비활성) + MinIO + pg-boss. 세션은 PG `user_session` 테이블, 임베딩 캐시는 `embed_cache` 테이블, rate-limit은 in-memory Map. 5000명 규모 배포를 목표로 한다. - 웹 앱: `apps/web` (Next.js, port 3010) - 백그라운드 워커: `apps/worker` (pg-boss)

### `CLAUDE.md`

Headings: # Jarvis — Claude Code Guide, ## 하네스: Jarvis Feature Development

Excerpt: # Jarvis — Claude Code Guide 사내 업무 시스템 + LLM 컴파일 위키 통합 (Karpathy LLM Wiki 방식). Next.js 15 모노레포(`apps/web`, `apps/worker`, `packages/*`). ## 하네스: Jarvis Feature Development **목표:** Jarvis 하네스는 **도메인 지식과 방향성만** 담당하고, 개발 방법론(계획·TDD·실행·리뷰·완료 검증·디버깅·병렬 디스패치·브랜치 마감)은 **superpowers 플러그인에 위임**한다. 얇은 진입점(`jarvis-feature`) + 도메인 레퍼런스 스킬 4개. **트리거:** Jarvis 프로젝트에서 기능 추가·수정·버그 수정·리팩토링·스키마 변경·번역 추가·권한 변경 등 구현 작업을 요청받으면 `jarvis-feature` 스킬을 사용하라. 단일 파일 1~2줄 수정이나 질문은 직접 응답해도 된다. **구성 요소:** - 에이전트: 없음 (방법론은 superpowers 서브에이전트 템플릿 사용) - 스킬: `.claude/skills/jarvis-feature/` (얇은 진입점 오케스트레이터), `.claude/skills/jarvis-architecture/` (모노레포·영향도 체크리스트·파일 변경 순서·검증 게이트), `.claude/skills/jarvis-db-patterns/` (31 스키마·34 권한·sensitivity·경계면 교차 비교), `.claude/skills/jarvis-i18n/` (ko.json·보간 변수), `.claude/skills/jarvis-wiki-feature/` (Karpathy 경계)

### `WIKI-AGENTS.md`

Headings: # WIKI-AGENTS — Jarvis LLM Wiki Schema, ## 0. 철학 한 문장, ## 1. 3-레이어 모델, ## 2. 디렉터리 구조

Excerpt: # WIKI-AGENTS — Jarvis LLM Wiki Schema > 이 파일은 Jarvis에서 **LLM이 사내 위키를 관리자처럼 운영**하기 위한 최상위 스키마·워크플로 규약이다. > Karpathy의 [LLM Wiki gist](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)를 엔터프라이즈 멀티테넌트 환경으로 확장한 것. > `CLAUDE.md`·`AGENTS.md`가 **코드 하네스**를 규정한다면, 이 파일은 **지식 하네스**를 규정한다. > > **상태:** v1 초안 (2026-04-15). 사용자+LLM이 함께 진화시키는 살아있는 문서. --- ## 0. 철학 한 문장

### 문서/워크플로 후보

- `docs/analysis/01-graphify.md`
- `docs/analysis/02-llm_wiki.md`
- `docs/analysis/03-llm-wiki-agent.md`
- `docs/analysis/04-mindvault.md`
- `docs/analysis/05-qmd.md`
- `docs/analysis/99-integration-plan-v4.md`
- `docs/analysis/README.md`
- `docs/audit/rsc-boundary-baseline.md`
- `docs/design-system.md`
- `docs/plan/2026-04-17-search-hybrid-page-embedding.md`
- `docs/plan/2026-04-17-tsmt001-infra-pipeline.md`
- `docs/plan/2026-04-17-tsvd999-wiki-pipeline.md`
- `docs/plan/2026-04-19-Jarvis_openai연동가이드.md`
- `docs/plan/2026-04-19-cliproxy-todo.md`
- `docs/plan/2026-04-W1-gate.md`
- `docs/plan/2026-04-W2-gate.md`
- `docs/plan/2026-04-W3-gate.md`
- `docs/policies/llm-models.md`
- `docs/superpowers/plans/2026-04-20-admin-users-extension.md`
- `docs/superpowers/plans/2026-04-20-contractor-management.md`
- `docs/superpowers/plans/2026-04-20-llm-first-retrieval.md`
- `docs/superpowers/plans/2026-04-20-projects-rename-and-add-dev.md`
- `docs/superpowers/plans/2026-04-21-multi-provider-llm-integration.md`
- `docs/superpowers/plans/2026-04-21-p0-p1-stabilization.md`
- `docs/superpowers/plans/2026-04-23-ask-harness-transition.md`
