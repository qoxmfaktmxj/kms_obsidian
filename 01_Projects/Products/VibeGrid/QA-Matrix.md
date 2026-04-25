# QA Matrix - VibeGrid

## 점검 기준

- 점검일: 2026-04-25 UTC
- repo: `/root/dev/qoxmfaktmxj/vibe-grid`
- 확인 파일: `README.md`, `AGENTS.md`, `CHANGELOG.md`, `package.json`, `scripts/run-core-tests.mjs`, `packages/*/src/index.ts`, `tests/e2e/*.spec.ts`, `packages/*/src/*.test.ts`
- 실행 시도: `npm run test:core`
  - 결과: 실패
  - 원인: `node_modules` 및 `node_modules/.bin/tsc` 없음. `npx tsc`가 TypeScript compiler 대신 `tsc@2.0.4` placeholder를 받아 실패.
  - 코드 실패 근거는 아니며, 의존성 설치 전 검증 환경 미준비 상태로 판단.

## Package scripts

| script | 역할 | 현재 판단 |
|---|---|---|
| `npm run lint` | packages/playground/bench lint | UI/패키지 변경 시 필수 |
| `npm run build` | playground + bench build | release gate |
| `npm run test:core` | TypeScript compile 후 Node unit tests | 현재 node_modules 미설치로 실행 실패 |
| `npm run test:e2e` | Playwright 전체 | browser regression 표준 |
| `npm run test:e2e:smoke` | hub/compatibility/bench smoke | 빠른 브라우저 회귀 |
| `npm run ci` | lint + build + core + e2e | 권장 full gate |

## Coverage matrix

| 영역 | 구현 근거 | Unit | E2E | 상태 | Gap |
|---|---|---:|---:|---|---|
| row state / save bundle | `packages/core/src/row-state.ts`, `contracts.ts` | 간접 | ✅ `grid-lab.spec.ts` save/delete | 양호 | row-state 순수 unit 직접 보강 여지 |
| bulk orchestration | `packages/core/src/bulk-orchestration.ts` | ✅ `bulk-orchestration.test.ts` | ✅ `employee-batch.spec.ts` | 실험 기능 기준 양호 | VibeHR 표준 채택 전 payload/permission 정책 필요 |
| React bulk hook | `packages/react/src/useGridBulkOrchestration.ts` | ✅ `useGridBulkOrchestration.test.ts` | ✅ employee batch 간접 | 실험 기능 기준 양호 | hook 소비 예제/실패 복구 시나리오 보강 |
| selection / range | `packages/core/src/selection.ts`, `VibeGrid.tsx` | 간접 | ✅ keyboard/drag/range copy | 양호 | selection 순수 unit 추가 가능 |
| header menu | `VibeGridTableHeader`, `VibeGridHeaderMenu` | 없음 | ✅ click/right-click/pin/sort/hide/resize/reload | 양호 | pinned+filtered+heavy scroll 조합 |
| filter row | `VibeGridFilterRow` | 없음 | ✅ apply/clear/select/focus/i18n | 양호 | number invalid 케이스 추가 |
| clipboard paste | `packages/clipboard/src/index.ts`, `VibeGrid.tsx` | 없음 | ✅ direct paste, append/reject, readonly, validation, range copy | 중상 | `parseTsv`, row/column overflow, appended row plan unit 보강 |
| Excel export/import/template | `packages/excel/src/index.ts`, `excel-client.ts` | 없음 | ❌ 직접 없음 | 취약 | buffer roundtrip, header mismatch, required schema test 필요 |
| persistence column state | `packages/persistence/src/index.ts`, Playground localStorage | 없음 | ✅ pin/width/hide reload | 중간 | storage key sanitize, invalid JSON fallback, scope isolation unit 필요 |
| virtualization/performance | `packages/virtualization/src/index.ts`, `RealGridPerformanceLab` | 없음 | ✅ 100k rendered row count/metrics | 양호 | threshold-based perf guard는 아직 약함 |
| date editor | `date-policy.ts`, `VibeGridDateEditor` | 없음 | ✅ constraints/i18n/KST regression | 중상 | date-policy helper unit 보강 |
| i18n | `packages/i18n/src/index.ts` | 없음 | ✅ filter/date labels 일부 | 중간 | message key completeness unit 필요 |
| theme tokens | `packages/theme-shadcn/src/index.ts` | 없음 | 간접 | 실험 | token naming 안정화 전 표준화 금지 |
| tree/group/pivot | `tree.ts`, `experimental-views.ts`, compatibility lab | 없음 | ✅ compatibility tree toggle/preview | 실험 | VibeHR 표준 기능 채택 금지 |
| public events | `events.ts`, Playground public event log | 없음 | ✅ paste/copy/save log | 실험 | event payload naming/ordering 안정화 필요 |

## E2E inventory

- `tests/e2e/hub-smoke.spec.ts`
  - Hub → Grid Lab / Employee Batch / Bench / Compatibility navigation
- `tests/e2e/grid-lab.spec.ts`
  - insert/copy/save, delete-check, HeaderCheck, paste append/reject, filter row, i18n, date editor, range copy, public events, readonly editability, single-click edit
- `tests/e2e/grid-header-menu.spec.ts`
  - header menu open/close, filtered indicator, pin, resize, reload persistence, sort, hide
- `tests/e2e/bench.spec.ts`
  - 100k real grid path, density, HeaderCheck, shift range, filter, pin, paste, delete, save bundle
- `tests/e2e/employee-batch.spec.ts`
  - 15,000 rows, exact 10,000 selection snapshot, sync/async execution, paging/sort, mutation plan
- `tests/e2e/compatibility.spec.ts`
  - IBSheet8 matrix, group/tree/pivot preview, tree runtime toggle, public-event parity 표시

## Unit inventory

- `packages/core/src/bulk-orchestration.test.ts`
  - selection snapshot order/duplicate/empty validation
  - mutation execution order
  - async result validation
  - request lane validation
- `packages/react/src/useGridBulkOrchestration.test.ts`
  - reducer state transitions
  - async/sync completion
  - error/reset
  - snapshot drift

## 취약 영역 우선순위

1. **Excel**
   - 자동 테스트 직접 커버 없음.
   - 실제 HR 업무 이식에서 template/upload/download는 표준 toolbar 핵심이므로 가장 먼저 보강 필요.
2. **Persistence**
   - reload e2e는 있으나 storage adapter unit이 없다.
   - VibeHR 사용자/화면별 scope 충돌 방지가 중요하다.
3. **Clipboard 순수 함수**
   - 브라우저 회귀는 비교적 충분하지만, paste engine의 순수 함수 조합은 unit이 없다.
   - 대량 TSV/validation/append 정책 회귀를 빠르게 잡기 어렵다.

## 다음 테스트 보강 후보

1. `packages/excel/src/index.test.ts`
   - template/export/import roundtrip
   - hidden `__schema` sheet 존재
   - header mismatch 시 `ok=false`, `missingHeaders`, `unknownHeaders` 검증
2. `packages/persistence/src/index.test.ts`
   - `namespace/appId/userId/gridId` key 생성
   - segment sanitize
   - invalid JSON fallback null
   - scope isolation
3. `packages/clipboard/src/index.test.ts`
   - CRLF/empty trailing line TSV parsing
   - `reject` vs `append` row overflow
   - readonly/hidden/validation skip counts
   - parser exception → validation error
