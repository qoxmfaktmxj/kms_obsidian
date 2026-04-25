# VibeHR Integration - VibeGrid

## 현재 결론

VibeGrid는 내부 파일럿 화면에는 사용할 수 있지만, VibeHR의 AG Grid 표준 화면을 즉시 전면 대체하기에는 아직 이르다.

권장 방향은 **전면 교체가 아니라 VibeHR 내부 파일럿 1개 화면/랩에서 VibeGrid adapter를 검증**하는 것이다.

## VibeHR 현재 표준과 충돌 지점

VibeHR 문서 기준 현재 grid 표준은 AG Grid `standard-v2`다.

- 화면 조건:
  - `AgGridReact` 사용
  - page 파일 `GRID_SCREEN` metadata 선언
  - `config/grid-screens.json` 등록
- toolbar 순서:
  - `query -> create -> copy -> template -> upload -> save -> download`
- row status:
  - `_status`, `_original`, `_prevStatus`
- dirty-row protection:
  - query/search/page/filter/data reload 전 확인 dialog 필수
- 검증 gate:
  - `npm run validate:grid`
  - `npm run lint`
  - `npm run build`
- action permission 표준 코드:
  - `query`, `create`, `copy`, `template_download`, `upload`, `save`, `download`

따라서 VibeGrid를 이식하려면 단순 컴포넌트 교체가 아니라 **VibeHR grid standard adapter**가 필요하다.

## VibeGrid → VibeHR mapping

| VibeHR 요구 | VibeGrid 대응 | 상태 |
|---|---|---|
| query/search | `GridQuery`, `onFiltersChange`, host-side fetch | adapter 필요 |
| create | `createInsertedRow`, `VibeGrid` edit session | 가능 |
| copy | `copyRow` command / row copy flow | 가능, public event는 experimental |
| template_download | `createExcelTemplateBuffer` | 가능하나 QA 취약 |
| upload | `importExcelPreview` + paste/apply flow | 가능하나 QA 취약 |
| save | `buildSaveBundle` | 가능 |
| download | `exportRowsToExcelBuffer` | 가능하나 QA 취약 |
| row status | `RowState: N/I/U/D` | `_status` adapter 필요 |
| dirty-row guard | VibeGrid 자체가 아니라 host shell 책임 | VibeHR wrapper 필수 |
| action permission | VibeHR `useMenuActions(path)` 기준 | toolbar wrapper 필요 |
| pagination contract | VibeHR API `page`, `limit`, `total_count` | host fetch adapter 필요 |
| grid registry | `config/grid-screens.json`은 현재 `engine: ag-grid` | VibeGrid pilot용 registry 정책 필요 |

## 선결 조건

### 1. 소비 import allowlist 확정

VibeHR에서 허용할 import를 먼저 고정한다.

허용 후보:

- `@vibe-grid/core`
- `@vibe-grid/react`
- `@vibe-grid/clipboard`
- `@vibe-grid/persistence`
- `@vibe-grid/excel` — 테스트 보강 후
- `@vibe-grid/i18n`
- `@vibe-grid/theme-shadcn`

금지/주의:

- `@vibe-grid/tanstack-adapter`
- `@vibe-grid/testing`
- `@tanstack/react-table` 직접 import
- `VibeGridProps.tree`, `useGridBulkOrchestration`, `publicEvents`를 표준 화면 기능으로 고정하는 것

### 2. VibeHR wrapper 설계

VibeHR 쪽에 `VibeGridStandardScreen` 같은 wrapper가 필요하다.

필수 책임:

- VibeHR toolbar order 유지
- `useMenuActions(path)` 기반 버튼 hide/disable/click block
- dirty-row protection dialog 연결
- VibeHR row status `_status/_original/_prevStatus` ↔ VibeGrid `RowState/GridRowMeta` 변환
- VibeHR API pagination (`page`, `limit`, `total_count`) ↔ `GridQuery/GridServerResult` 변환
- localStorage scope: `namespace=아예-vibe-hr`, `appId`, `gridId`, `userId`

### 3. Excel QA 보강

VibeHR toolbar의 `template/upload/download`는 필수 액션이다. 현재 VibeGrid Excel 자동화 테스트가 없어 선결 보강이 필요하다.

필수 테스트:

- export buffer 생성 후 workbook header 검증
- template buffer의 hidden `__schema` sheet 검증
- import preview header mismatch 검증
- roundtrip: template → import preview → paste text 생성

### 4. Persistence scope 보강

VibeHR은 사용자/메뉴/화면 단위로 컬럼 상태가 충돌하면 안 된다.

필수 테스트:

- `namespace/appId/userId/gridId` 별 key 분리
- 특수문자 sanitize
- invalid JSON 복원 실패 시 null fallback
- 다른 화면 scope 간 state isolation

### 5. Clipboard 대량/권한 정책 정리

VibeHR 업무 화면은 Excel/clipboard 대량 입력이 핵심이다.

필수 정리:

- row overflow 기본값: `reject` 유지 권장
- append는 명시적 화면 정책이 있을 때만 허용
- readonly/hidden/validation skip summary를 VibeHR status UI와 연결
- 권한 없는 upload/paste는 UI와 server action gate 양쪽에서 차단

## 추천 pilot 순서

1. VibeGrid repo에서 Excel/Persistence/Clipboard unit test 보강
2. VibeHR에 코드 반영 전 adapter 설계 문서 작성
3. 기존 핵심 AG Grid 화면을 바로 교체하지 말고 내부 lab route 또는 낮은 위험의 HR 보조 화면에서 검증
4. 성공 후 `hr.employee` 같은 대표 화면은 별도 R2 승인 하에 vertical slice로 진행

## 대체 기준

VibeGrid가 VibeHR 표준 교체 후보가 되려면 아래가 닫혀야 한다.

- Public API allowlist 문서화
- Excel/Persistence/Clipboard 최소 unit coverage
- VibeHR dirty-row protection wrapper
- VibeHR menu action permission wrapper
- `validate:grid`에 VibeGrid pilot screen 검증 전략 반영 여부 결정
- Playwright로 query/create/copy/template/upload/save/download 전체 toolbar flow 검증
