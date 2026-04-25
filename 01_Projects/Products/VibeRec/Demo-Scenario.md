# Demo-Scenario

_Last updated: 2026-04-25 UTC_

## 데모 판정

- **지원자 데모:** 가능
- **관리자 읽기 데모:** 가능
- **관리자 운영 액션 데모:** 현재 UI에서는 불가

관리자 상세의 상태변경/면접/최종결정 컴포넌트와 API는 존재하지만 `/admin/applicants/[id]` page에 연결되어 있지 않다. 데모에서 해당 버튼을 누르는 장면은 아직 피해야 한다.

## 준비

README 기준:

```powershell
docker compose -f compose.deploy.yaml up -d postgres
cd apps/api
.\gradlew.bat bootRun --args=--server.port=8080
cd apps/web
$env:API_BASE_URL="http://127.0.0.1:8080/api"
$env:NEXT_PUBLIC_API_BASE_URL="http://127.0.0.1:8080/api"
npm run dev
```

Demo seed:

- Flyway: `apps/api/src/main/resources/db/migration/V25__refresh_realistic_demo_dataset.sql`
- 수동 seed: `apps/api/src/main/resources/db/seed/demo-seed.sql`
- Hotspot: `1001 / platform-backend-engineer / 백엔드 플랫폼 엔지니어`
- README 기준 데모 지원자: `5,000명`

## 지원자 시나리오 — 현재 가능

1. `/job-postings`
   - 공고 목록, 검색, 지원 가능 공고 필터를 보여준다.
2. `/job-postings/{id}`
   - 공고 상세, 채용 단계, 내 지원 현황 카드를 보여준다.
3. 비로그인 상태에서 지원 클릭
   - `/auth/login?next=/job-postings/{id}/apply` 복귀 흐름을 보여준다.
4. `/profile`
   - 프로필 선작성 화면을 보여준다.
   - 주의: 자기소개/핵심강점 템플릿은 지원서 Step2 자동 import까지는 미완성.
5. `/job-postings/{id}/apply`
   - 4-step 지원 위저드 진행.
   - Step3에서 `프로필에서 가져오기` 가능.
   - 임시저장 가능.
6. 최종 제출
   - 성공 시 `/me?submitted=1`로 이동.
7. `/me`
   - 완료 배너와 내 지원 목록 확인.
8. `/me/applications/{applicationId}`
   - 제출한 지원서 읽기 전용 확인.

## 관리자 시나리오 — 현재 안전하게 보여줄 수 있는 범위

1. `/admin/login`
   - 관리자 로그인.
2. `/admin`
   - 공고 관리 대시보드, 공고 수/공개/모집중 요약.
   - 공고 등록/수정/질문 관리 버튼 존재.
3. `/admin/job-postings/new`
   - 공고 등록 폼 확인.
4. `/admin/job-postings/{id}`
   - 공고 수정 폼 확인.
5. `/admin/job-postings/{id}/questions`
   - 지원 문항 관리 확인.
6. `/admin/applicants`
   - 지원자 목록, 통합 검색, 공고/상태/검토상태 필터, 페이지네이션 확인.
7. `/admin/applicants/{applicationId}`
   - 지원자 상세, 상태 뱃지, 이력서 상세, 원본 데이터, 첨부파일 확인.

## 현재 데모 금지/주의 구간

| 구간 | 현재 상태 | 데모 리스크 |
|---|---|---|
| 지원자 상세에서 심사 상태 변경 | API/BFF/컴포넌트 존재, page 미연결 | 버튼이 없어 진행 불가 |
| 면접 등록/완료/평가 | API/BFF/컴포넌트 존재, page 미연결 | 데모 흐름 중단 |
| 최종결정 | API/BFF/컴포넌트 존재, page 미연결 | 합격 이후 결과 마무리 불가 |
| 프로필 템플릿 → 지원서 Step2 | 프로필 저장은 가능, Step2 import 없음 | “반복 활용” 메시지 약화 |

## 데모 토크 트랙

- “지원자는 공고를 보고, 계정으로 로그인한 뒤, 프로필과 지원서를 한 흐름으로 작성합니다.”
- “제출 후에는 내 지원 내역에서 상태와 제출 내용을 다시 확인할 수 있습니다.”
- “관리자는 대량 지원자를 검색/필터하고 상세 정보를 볼 수 있습니다.”
- “다음 구현으로 이미 존재하는 심사/면접/최종결정 API와 컴포넌트를 상세 화면에 연결하면 운영 액션까지 닫힌 데모가 됩니다.”

## 데모 완성 조건

- [ ] 관리자 상세에서 심사 상태를 `NEW → IN_REVIEW → PASSED/REJECTED`로 변경 가능
- [ ] `PASSED` 후 면접 등록/완료/평가 가능
- [ ] 최종결정 `OFFER_MADE → ACCEPTED/DECLINED` 가능
- [ ] 위 흐름을 seed 데이터로 1회 리허설 완료
