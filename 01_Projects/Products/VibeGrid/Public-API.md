# Public API - VibeGrid

## 점검 기준

- 점검일: 2026-04-25 UTC
- 대상 repo: `/root/dev/qoxmfaktmxj/vibe-grid` (`master`, `origin/master` 동기화 상태)
- 범위: 코드 수정 없음. README/AGENTS/CHANGELOG/package scripts/packages/*/src/index.ts/tests/e2e/unit tests 기준 문서 점검.

## 현재 공개 API 원칙

VibeGrid의 제품 원칙은 명확하다.

1. 소비 앱은 `@vibe-grid/react`와 `@vibe-grid/core`를 중심으로 사용한다.
2. TanStack Table은 내부 엔진이며 소비 앱에 직접 노출하지 않는다.
3. `apps/playground`, `apps/bench`, `packages/testing`은 검증/실험 표면이지 앱 이식 API가 아니다.
4. Stable/Experimental 경계는 `docs/release/public-api-stability.md`를 기준으로 판단한다.

## Package export 현황

| 패키지 | export entry | 앱 노출 판단 | 근거 |
|---|---|---:|---|
| `@vibe-grid/core` | `./src/index.ts` | Stable + Experimental 혼재 | `packages/core/src/index.ts`, `docs/release/public-api-stability.md` |
| `@vibe-grid/react` | `./src/index.ts` | 주 소비 표면 | `packages/react/src/index.ts`, `packages/react/src/VibeGrid.tsx` |
| `@vibe-grid/clipboard` | `./src/index.ts` | 실무 앱에서 필요 | `packages/clipboard/src/index.ts` |
| `@vibe-grid/excel` | `./src/index.ts` | 실무 앱에서 필요하나 QA 취약 | `packages/excel/src/index.ts` |
| `@vibe-grid/persistence` | `./src/index.ts` | 컬럼 상태 한정 사용 가능 | `packages/persistence/src/index.ts` |
| `@vibe-grid/i18n` | `./src/index.ts` | 공유 메시지 표면 | `packages/i18n/src/index.ts` |
| `@vibe-grid/theme-shadcn` | `./src/index.ts` | 테마 토큰 실험성 주의 | `packages/theme-shadcn/src/index.ts` |
| `@vibe-grid/tanstack-adapter` | `./src/index.ts` | 내부 전용에 가깝다 | `packages/tanstack-adapter/src/index.ts` |
| `@vibe-grid/virtualization` | `./src/index.ts` | 내부/고급 전용 | `packages/virtualization/src/index.ts` |
| `@vibe-grid/testing` | `./src/index.ts` | 앱 소비 금지 권장 | `packages/testing/src/index.ts` |

## Stable for pilot use

현재 파일 기준으로 파일럿 소비 앱에 허용 가능한 표면이다.

- `@vibe-grid/core`
  - `VibeGridColumn`, `ManagedGridRow`, `GridQuery`, `GridFilter`, `GridSortRule`
  - row state/save bundle: `createLoadedRow`, `createInsertedRow`, `applyRowPatch`, `buildSaveBundle`, `markRowsSaved`
  - selection/range: `GridSelectionState`, `createSelectionState`, range helpers
  - column state: `GridColumnState`, `createGridColumnState`, `sanitizeGridColumnState`, pin/width/visibility/order helpers
  - editability/validation/date policy helpers
- `@vibe-grid/react`
  - `VibeGrid`
  - `VibeGridProps` 중 안정 영역: `rows`, `columns`, `selectionState`, edit session, `columnState`, sorting/filter props, `enableFilterRow`, `enableRowCheck`, `density`, `virtualization`
  - `resolveGridDensityMetrics`
- `@vibe-grid/clipboard`
  - `parseTsv`, `createClipboardSchema`, `buildRectangularPastePlan`, `summarizeRectangularPastePlan`
- `@vibe-grid/persistence`
  - `createGridPreferenceStorageKey`, `createBrowserGridPreferenceAdapter`
  - 범위는 column state 한정
- `@vibe-grid/excel`
  - `createGridExcelSchema`, `validateExactHeaders`, `exportRowsToExcelBuffer`, `createExcelTemplateBuffer`, `importExcelPreview`
  - 단, 현재 자동화 테스트가 부족하므로 VibeHR 선이식 전 보강 필요

## Experimental / churn 가능 영역

다음은 root export에 존재하지만 broad rollout 기준으로는 잠금 금지다.

- `@vibe-grid/core`
  - bulk orchestration 계열: `GridBulkOrchestrationRequest`, `createGridSelectionSnapshot`, `buildGridMutationExecutionPlan`, `validateGridExecutionResult`
  - tree runtime: `GridTreeSpec`, `GridTreeState`, `shapeGridTreeRows`, `toggleGridTreeRowExpanded`
  - group/tree/pivot preview: `buildGridGroupPreview`, `flattenGridTree`, `buildGridPivotPreview`
  - `GridPublicEventHandlers`, `onBeforePaste`, `onAfterPaste`, `onAfterSave`, `onAfterRowCopy`
- `@vibe-grid/react`
  - `useGridBulkOrchestration`
  - `VibeGridProps.tree`
  - `publicEvents`
- `@vibe-grid/theme-shadcn`
  - token naming 전체
- `@vibe-grid/testing`
  - Bench/Lab 컴포넌트 전체

## 내부 구현 노출 위험

| 위험 | 현재 상태 | 영향 | 조치 제안 |
|---|---|---|---|
| Stable/Experimental이 같은 root index에서 함께 export됨 | `core/src/index.ts`, `react/src/index.ts`에 experimental export 포함 | 소비 앱이 실험 기능을 안정 API로 오해 가능 | 문서/README에 “allowed import list” 고정, 장기적으로 `experimental` subpath 분리 검토 |
| `@vibe-grid/tanstack-adapter`가 package export로 열려 있음 | `createTanStackColumns`가 `ColumnDef`를 반환 | 소비 앱이 TanStack 타입을 직접 의존할 수 있음 | VibeHR 이식 문서에서 소비 금지 명시, 필요 시 package visibility/문서 경고 강화 |
| `@vibe-grid/react` 내부에 TanStack dependency 존재 | props에는 TanStack 타입 노출 없음 | 직접 노출 위험은 낮지만 내부 구조 복사 위험 | 앱에서 `useReactTable` 직접 import 금지 유지 |
| `VibeGridProps.tree/publicEvents`가 이름상 experimental 표시 없음 | 안정 문서에서만 experimental로 분류 | 앱 코드가 실험 기능에 묶일 수 있음 | prop JSDoc 또는 별도 문서 경고 필요 |
| `@vibe-grid/testing` export가 소비 가능 | RealGridPerformanceLab/BenchWorkbench export | 앱 번들에 lab 코드 유입 가능 | VibeHR vendor import allowlist에서 제외 |

## 취약 영역 판단

1. **Excel: 가장 취약**
   - `packages/excel/src/index.ts`는 xlsx export/import/template 기능을 제공하지만 unit/e2e 직접 커버가 확인되지 않았다.
   - Grid Lab에는 Excel 버튼과 lazy client가 있으나 `tests/e2e/grid-lab.spec.ts`에서 다운로드/업로드 roundtrip 검증은 없다.
2. **Persistence: 중간 취약**
   - header menu e2e에서 pin/width/hide reload persistence가 검증된다.
   - 하지만 `createGridPreferenceStorageKey`, JSON parse fallback, scope sanitization unit test는 없다.
3. **Clipboard: 상대적으로 강함**
   - direct paste, append/reject overflow, readonly skip, invalid parse summary, range copy가 e2e로 검증된다.
   - 단, `parseTsv`/rectangular plan 순수 함수 unit test는 별도로 없다.

## 권장 소비 규칙

- VibeHR 이식 1차 allowlist:
  - `@vibe-grid/core`
  - `@vibe-grid/react`
  - `@vibe-grid/clipboard`
  - `@vibe-grid/persistence`
  - `@vibe-grid/excel`은 테스트 보강 후
  - `@vibe-grid/i18n`
  - `@vibe-grid/theme-shadcn`
- VibeHR 이식 금지/주의:
  - `@vibe-grid/tanstack-adapter`: VibeGrid 내부 변경 외 소비 금지
  - `@vibe-grid/testing`: 앱 소비 금지
  - `@tanstack/react-table` 직접 import 금지
  - `tree`, `bulk orchestration`, `publicEvents`는 명시적 파일럿 승인 전 표준 기능으로 채택 금지
