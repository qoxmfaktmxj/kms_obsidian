---
created: 2026-04-27
source: claude
tags: [jarvis, dashboard, merge, post-merge-report, lounge-chat, design-overhaul, phase2-t2]
project: Jarvis
status: shipped
prs: [25, 27]
---

# Jarvis Dashboard Redesign — Main 머지 완료 보고서

> **TL;DR**: 30-task 대시보드 개편 작업(채팅+위젯+계약직 master-detail)을 main에 머지. 35커밋(원래 작업) + 3커밋(merge/token migration/Server Action 분리) + 1커밋(P2 follow-up) = **총 39커밋** 반영. CI 전부 통과, 독립 코드리뷰 P0/P1 없음.

## 핵심 결과

| 항목 | 값 |
|------|-----|
| Base | `31b4c38` (PR #25 직전 main) |
| Final main | `7626f7f` |
| PR #25 merge | `2af4f59` (대시보드 본체) |
| PR #27 merge | `7626f7f` (NoticesWidget cleanup, P2) |
| 머지 시각 | 2026-04-27 06:40 UTC |
| Repo | https://github.com/qoxmfaktmxj/jarvis |

## 작업 발단

사용자가 **대시보드 개편 작업물(채팅 추가 + 디자인 변경)** 을 작업하다 멈춘 채로 잊고 있었음. 그 사이 main에는 **Jarvis 디자인 전면개편(Phase 1/2 Notion 토큰)** 과 **Ask AI Harness Phase D+E(embedding 파이프라인 전면 제거)** 가 머지됨. 결과적으로 작업 브랜치 `claude/flamboyant-chandrasekhar-1964b4`이 main 대비 35커밋 앞선 채 stale 상태.

순서: **대시보드 작업 (멈춤) → main 디자인 개편 → 본 작업(merge + 마감)**.

## 주요 결정 (AI 참고용)

### 1. rebase 대신 merge 선택
- 35커밋 rebase는 충돌 누적 위험 큼 → `git merge main` 1회로 처리
- 결과: 충돌 8건만 발생, 모두 단순 해소

### 2. 충돌 해소 전략
| 충돌 | 처리 |
|------|------|
| 5개 레거시 위젯(`MyTasksWidget`/`QuickLinksWidget`/`RecentActivityWidget`/`SearchTrendsWidget`/`StalePagesWidget`) + `StatCard` | **삭제** (브랜치 의도, 844ef35에서 이미 제거 의도) — main 쪽은 Notion 토큰 마이그레이션만 한 죽은 변경 |
| `packages/db/schema/index.ts` | main의 `embed-cache` 제거 + 대시보드의 `chat.js` export 둘 다 유지 |
| `packages/db/drizzle/_journal.json` | dashboard `0037` → **`0040` 재번호** (main의 0037-0039 뒤로) |
| `0037_flowery_outlaw_kid.sql` / 스냅샷 | `0040`으로 `git mv` |
| `.env.example` | auto-merged |

### 3. Phase 2 T2 토큰 정합화 (필수 사후 작업)
- **사용자가 까먹은 "디자인 변경"의 정체** = 대시보드 새 컴포넌트가 main의 Phase 2 T2 Notion 토큰 표준을 따르지 않은 채 stale ISU/surface 토큰 사용 중이었음
- 13파일/61줄을 **기계적으로 일괄 치환** (perl one-liner)
- 매핑 표: `docs/superpowers/plans/2026-04-25-design-overhaul-phase-2-T2.md` §0
- 핵심 룰:
  - `bg-isu-{50,600,700}` → `bg-[--brand-primary{,-bg,-hover}]`
  - `text-surface-{700,800,900}` → `text-[--fg-primary]` (strict, secondary 아님)
  - `bg-card`/`text-foreground`/`text-destructive` shadcn alias도 함께 정리

### 4. Server Actions 비동기 강제 (Next 15)
- **빌드 단계에서 발견** (type-check는 통과했으나 webpack에서 실패)
- `"use server"` 파일은 **모든 export가 async여야** 함
- 동기 validator(`validateSend/Toggle/Delete`, `validateBatchBusinessRules`, `leaveBatchInputSchema`)를 **`*.validators.ts`로 분리**:
  - `apps/web/app/actions/chat.ts` → `chat.validators.ts`
  - `apps/web/app/(app)/contractors/leaves/actions.ts` → `actions.validators.ts`
- 테스트 import 경로도 함께 수정 (`./chat.js` → `./chat.validators.js`)

## 검증 게이트 결과 (Task 30)

| 게이트 | 결과 | 비고 |
|--------|------|------|
| `node scripts/check-schema-drift.mjs --precommit` | ✅ | drift 없음 |
| `pnpm type-check` ×2 | ✅ 10/10 packages | 26.5s → 14.7s (2회차 캐시 hit) |
| `pnpm lint` | ✅ | warning만 (기존 코드 unused vars: `actorId`, test util) |
| `pnpm test` ×2 | ⚠️→✅ | 1회차 turbo cold-start로 sentry/wiki-ops-budget timeout(20s) flaky, 단독 실행 시 통과. 2회차 8/8 통과 |
| `pnpm build` (webpack) | ✅ 2/2 | Server Actions 수정 후 통과 |
| RSC boundary audit | ✅ | page=server async + Promise.all, interactive 5컴포넌트=client, props 직렬화 OK |
| pre-push hook (build) | ✅ | "Verification checks passed" |
| CI (PR #25) | ✅ 모두 통과 | type-check, unit-and-integration, schema-drift, docker-build (web/worker), legacy-body-grep |

## 코드 리뷰 결과 (code-reviewer agent, 독립 리뷰)

- **P0/P1 없음** → go-ahead
- **P2 (2건)**:
  1. `NoticesWidget.tsx`의 `badgeFor()` 가 dead `label` 필드 반환 (JSX는 `t()` 직접 사용) → **PR #27로 정리 완료**
  2. drizzle `0037`/`0038`/`0039` 스냅샷이 main에 사전 누락 — **이번 작업과 무관** (사전 존재). drizzle-kit에 backfill 표준 명령 없어서 위험. schema-drift는 통과하므로 그대로 둠
- **P3 (2건)**:
  1. `chat-listen-pool.ts` 의 `max=200` + `idleTimeoutMillis: 0` — 문서화 권장
  2. (token migration 정확성) 모든 `text-surface-700/800/900`가 `--fg-primary` 매핑 — 검증 완료
- **긍정 검증**:
  - workspace 격리 (모든 query/action에서 `session.workspaceId` 필터)
  - RBAC 2단계 (lookup → workspaceId 재확인 → 권한 체크)
  - SSE 라이프사이클 (heartbeat 15s, AbortSignal cleanup, dedicated pg Pool, channel naming UUID dashes→underscores)
  - validator 커버리지 (모든 server action이 mutation 전 validate)
  - i18n (Lounge/Vacations/Latest-Wiki 모두 namespace resolved)
  - race conditions (toggle/leave-batch 모두 transaction)

## Post-merge 정리

- 워크트리 제거: `.claude/worktrees/{dashboard-merge,p2-followup}`
- 로컬·원격 브랜치 삭제: `claude/flamboyant-chandrasekhar-1964b4`, `chore/dashboard-followup-p2`

## main에 새로 추가된 핵심 파일 (AI 검색용)

### 컴포넌트
```
apps/web/app/(app)/dashboard/_components/
  HeroGreeting.tsx (server)
  InfoCardRow.tsx (server)
  DateCard.tsx (server)
  TimeCard.tsx (client)
  WeatherCard.tsx (client, 10분 캐시 fetch)
  FxCard.tsx (client, 1시간 캐시 fetch)
  LoungeChat.tsx (client, SSE + optimistic)
  ChatComposer.tsx, ChatMessage.tsx (client)
  ReactionPopover.tsx, ReactionChipRow.tsx (client)
  NoticesWidget.tsx, VacationsWidget.tsx, LatestWikiWidget.tsx (server)
```

### 백엔드
```
apps/web/app/actions/chat.{ts,validators.ts,test.ts}
apps/web/app/(app)/contractors/leaves/actions.{ts,validators.ts,test.ts}
apps/web/app/api/chat/{online,reactions,send,stream}/route.ts
apps/web/app/api/{weather,fx}/route.ts
apps/web/lib/queries/{chat,dashboard-notices,dashboard-vacations,dashboard-wiki}.ts
apps/web/lib/db/chat-listen-pool.ts
packages/shared/chat/channel.ts
packages/shared/validation/chat.ts
packages/shared/constants/chat.ts
```

### DB
```
packages/db/schema/chat.ts (chat_message, chat_reaction)
packages/db/drizzle/0040_flowery_outlaw_kid.sql
packages/db/drizzle/meta/0040_snapshot.json
```

## 학습 포인트 (AI 향후 작업 시 참고)

1. **Stale 브랜치 머지 전 항상 main → 브랜치로 먼저 머지**: 본 작업처럼 base 디자인이 바뀐 경우 사후 정합화가 필수. dashboard 새 컴포넌트들의 Phase 2 T2 토큰 마이그레이션이 그 사례.

2. **Next 15 `"use server"` 파일은 모든 export = async 강제**: type-check는 통과해도 webpack build에서 잡힘. 동기 validator는 반드시 sibling `*.validators.ts`로 분리.

3. **Drizzle journal `idx` 재번호 시 SQL+snapshot 두 파일 모두 `git mv`**: `0037_*.sql` + `meta/0037_snapshot.json` → 둘 다 `0040`으로.

4. **modify/delete 충돌은 보통 "삭제 채택"이 정답**: 파일을 삭제한 쪽의 의도가 명시적, 변경한 쪽은 의도하지 않은 잔존 가능성.

5. **Turbo 병렬 test 1회차 flaky → 2회차 강제 실행 룰 유효**: vitest worker contention으로 cold-start timeout 발생. 단독 실행은 통과하므로 panic하지 말 것.

6. **사용자가 "디자인 변경"이라 모호하게 말할 때**: 토큰/디자인 시스템 차이일 가능성 큼. base와 head의 디자인 phase 차이부터 확인.

## 후속 작업 (보류)

- ❌ drizzle `0037-0039` 스냅샷 backfill — 위험 대비 가치 낮음, 그대로 둠
- ❌ chat-listen-pool `idleTimeoutMillis` 문서화 — P3, 시급성 낮음

## 관련 문서 (Jarvis 레포 내)

- 원본 30-task plan: `docs/superpowers/plans/2026-04-23-dashboard-redesign.md`
- 디자인 phase 2 T2 토큰 매핑: `docs/superpowers/plans/2026-04-25-design-overhaul-phase-2-T2.md` §0
- spec: `docs/superpowers/specs/2026-04-24-design-overhaul-design.md`
- preview HTML: `docs/superpowers/specs/previews/dashboard.html`

## 관련 노트 (vault 내)

- [[Jarvis]]
- [[Decisions]]
- [[LLM-Wiki-Architecture]]
- [[Current-Sprint]]
