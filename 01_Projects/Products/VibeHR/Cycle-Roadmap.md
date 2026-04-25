# VibeHR Cycle Roadmap

> 기준: 2026-04-25 UTC repo 실제 상태 분석. 코드 수정/커밋/푸시 없음.
> 필독 반영: `vibe-hr/AGENTS.md`, `config/grid-screens.json`, `docs/GRID_SCREEN_STANDARD.md`, `docs/MENU_ACTION_PERMISSION_PLAN.md`.

## 상태 요약

| Cycle | 현 상태 | 근거 | 주요 빈틈 |
|---|---:|---|---|
| 1. 합격자 → 사원 → 입사발령 | 부분 완성(약 75%) | 합격자 관리/사번채번/사원생성/발령확정 구현 | 합격자 `appointed` 자동 전환 없음, 채용-발령 완료 추적 약함 |
| 2. 근태 → 승인 → 월마감 | 부분 완성(약 65%) | 출퇴근/근태현황/정정/휴가승인/월마감/급여변수 생성 구현 | 근태 정정 승인 워크플로 부재, 월마감 lock 적용 범위 제한 |
| 3. 급여 → 계산 → 마감 | 부분 완성(약 80%) | Run 생성/대상자 snapshot/계산/마감/지급완료/명세 조회 구현 | 회계/지급 파일/마감 취소 부재, TIM 마감 선행조건 강제 약함 |
| 4. 복리후생 → 신청/승인 | 부분 완성(약 70%) | 본인신청/관리자 승인·반려/급여계산 반영 구현 | 지급완료/정산취소 상태 없음, payroll 반영 타이밍이 계산 시점에 묶임 |
| 5. 연말정산 | 미착수 | 관련 화면/API 확인 불가 | 별도 설계 필요 |

## Cycle 1: 합격자 → 사원 생성 → 입사발령

- [x] 채용 합격자 화면: `/hr/recruit/finalists`, `hr.recruit.finalists` standard-v2 등록.
- [x] 합격자 CRUD/IF 동기화/사번채번 API 존재.
- [x] 선택 합격자 사원 생성: `create_employees_from_finalists()`가 `HrEmployee` + `AuthUser` + 기본 프로필 생성.
- [x] 생성된 사원은 `employment_status="leave"`, 부서 `RECRUIT-STAGING`, 직위 `채용대기`로 생성되어 입사발령 전 대기 상태를 표현.
- [x] 발령 화면 이동: 합격자 화면에서 사번 기준 `/hr/appointment/records?employeeNo=...` 이동.
- [x] 입사발령 생성/확정: 발령 오더 확정 시 `HrEmployee`의 부서/직위/재직상태 변경 및 인사이력 생성.
- [ ] 합격자 상태 `ready → appointed`가 발령 확정과 자동 연동되지 않음.
- [ ] 발령번호/합격자ID/사원ID를 묶는 end-to-end trace가 약함.

### 다음 보강 후보
1. 발령 확정 시 `employee_no`로 합격자를 찾아 `status_code="appointed"` 자동 전환.
2. 합격자 화면에 “발령완료 여부/발령번호” 조회 컬럼 또는 상세 링크 추가.
3. `frontend/tests/e2e/hr-finalist-appointment.spec.ts`를 현재 API 흐름 기준으로 보강.

## Cycle 2: 근태 → 승인 → 월마감

- [x] 출퇴근 셀프서비스: `/tim/check-in` → `/api/tim/attendance-daily/check-in|check-out`.
- [x] 근태현황: `/tim/status`, `tim.attendance-status` standard-v2 등록.
- [x] 근태 정정: `/tim/correction`에서 관리자/HR 권한으로 상태·출퇴근 시각 정정 이력 저장.
- [x] 휴가 신청/승인: `/tim/leave-request`, `/tim/leave-approval`, approve/reject/cancel API 존재.
- [x] 월마감: `/tim/month-close` custom 화면 + API. 마감 시 근무시간 재계산 및 연장/야간/휴일수당 `PayVariableInput` 자동 생성.
- [x] 마감 후 근태 정정 차단: `assert_month_not_closed()`가 correction API에 적용.
- [ ] “근태 정정 요청 → 승인 → 반영” 상태 머신은 없음. 현재는 관리자 직접 정정.
- [ ] `tim.month-close`와 legacy `/tim/month-closing` 라우트/권한 path가 혼재.
- [ ] 월마감이 급여 Run 생성/계산의 필수 선행조건으로 강제되지 않음.

### 다음 보강 후보
1. 근태 정정 신청 테이블/상태(`submitted/approved/rejected`)와 승인 화면 분리.
2. `/tim/month-close` vs `/tim/month-closing` 라우트/메뉴/권한 path 정리.
3. Payroll Run 생성·계산 전 해당 월 TIM 마감 여부 검증.

## Cycle 3: 급여 대상자 생성 → 계산 → 마감

- [x] 급여 기초: 급여코드, 항목그룹, 수당/공제, 세율, 간이세액 구간, 지급일정, 사원급여프로필 화면 등록.
- [x] 급여 변수 입력: `/payroll/variable-inputs`, `/api/pay/variable-inputs/batch`.
- [x] Run 생성: `/payroll/runs`, `/api/pay/runs`.
- [x] 대상자 snapshot: 사원/급여프로필/발령/휴가/복리후생 이벤트를 `PayPayrollRunTarget`/event로 materialize.
- [x] 계산: 기본급 + 변수 + 복리후생 + 법정공제 계산 후 `PayPayrollRunEmployee/Item` 생성.
- [x] 마감/지급완료: `calculated → closed → paid` 상태 전이.
- [x] 명세 조회/PDF: 본인 및 관리자 PDF endpoint 존재.
- [ ] closed/paid 되돌리기, 지급파일/회계전표 인터페이스는 없음.
- [ ] TIM 월마감, 복리후생 승인마감 등 선행 마감 조건이 Run 상태 전이에 강제되지 않음.

### 다음 보강 후보
1. Run 생성/계산 전 checklist: TIM 월마감, 복리후생 승인건, 급여프로필 누락 검증.
2. closed run의 정정/재오픈 정책 설계.
3. 지급파일/회계전표 export 최소 포맷 설계.

## Cycle 4: 복리후생 신청 → 승인 → 지급/반영

- [x] 복리후생 유형: `/wel/benefit-types`, `wel.benefit-types` standard-v2 등록.
- [x] 본인 신청: `/wel/my-requests`, `/api/wel/requests`.
- [x] 관리자 승인/반려: `/wel/requests`, approve/reject API.
- [x] 급여 반영: Payroll 계산 시 approved/payroll_reflected 대상 복리후생을 급여 항목으로 반영하고 `status_code="payroll_reflected"`로 갱신.
- [ ] 급여 반영 후 취소/역분개/지급완료 별도 상태는 없음.
- [ ] 승인 이후 어느 급여월에 반영될지 사전 확정하는 workflow가 약함.

### 다음 보강 후보
1. 승인 시 반영예정월(`target_year_month`) 확정 필드 추가.
2. 급여 반영 후 취소 정책 및 조정 입력 생성 규칙 설계.
3. 신청/승인/급여반영 이력 timeline 제공.

## Cycle 5: 연말정산

- [ ] 별도 화면/API/모델 확인 필요.
- [ ] Payroll closed data를 기초로 한 연말정산 도메인 설계 필요.
