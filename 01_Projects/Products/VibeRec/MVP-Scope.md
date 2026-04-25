# VibeRec MVP Scope

_Last updated: 2026-04-25 UTC / repo static gap analysis_

## 목표

완성본에 가까운 첫 SaaS 데모로 만든다. 현재 코드는 **지원자 루프는 대체로 닫혀 있고**, **관리자 루프는 읽기/목록은 가능하지만 상세 화면의 변경 액션이 연결되지 않아 데모가 막힌다.**

## 근거 범위

- Repo: `/root/dev/qoxmfaktmxj/vibe-rec`
- 확인 문서: `README.md`, `AGENTS.md`, `DESIGN.md`, `docs/architecture.md`, `docs/auth-flows.md`
- 확인 구현: Next.js app routes/BFF, Spring API controller/service/domain, demo seed 문서

## Flow Verdict

| 플로우 | 현재 판정 | 데모 가능 여부 | 핵심 근거 |
|---|---:|---:|---|
| 공고 목록 → 상세 | ✅ 구현 | ✅ 가능 | `apps/web/src/app/job-postings/page.tsx`, `[id]/page.tsx`, `JobPostingController` |
| 프로필 작성 | ✅ 구현 | ✅ 가능 | `/profile`, `ProfileEditor`, `/api/candidate/profile`, `CandidateProfileService` |
| 프로필 → 지원서 불러오기 | ⚠️ 일부 구현 | ⚠️ 제한 | Step3 이력/스킬 계열만 불러옴. 자기소개/핵심강점 템플릿은 지원서 Step2로 자동 반영되지 않음. |
| 지원서 임시저장/제출 | ✅ 구현 | ✅ 가능 | `ApplicationWizard`, application-draft/application-submit BFF, `ApplicationDraftService` |
| 완료 화면/내 지원 | ✅ 구현 | ✅ 가능 | 제출 후 `/me?submitted=1`, `/me/applications/[applicationId]` 읽기 화면 |
| 관리자 공고 관리 | ✅ 구현 | ✅ 가능 | `/admin`, 공고 등록/수정/질문 관리, `AdminJobPostingService` |
| 관리자 지원자 목록/필터 | ✅ 구현 | ✅ 가능 | `/admin/applicants`, `AdminApplicantTable`, `AdminApplicantController` |
| 관리자 지원자 상세 조회 | ✅ 읽기 구현 | ✅ 읽기만 가능 | `/admin/applicants/[id]`에서 요약/이력서/첨부파일 표시 |
| 관리자 상태 변경 | ⚠️ API/컴포넌트만 존재 | ❌ 상세 UI에서 막힘 | `ApplicantReviewForm`과 BFF/API는 있으나 상세 page에 mount/import 없음 |
| 관리자 면접/평가 | ⚠️ API/컴포넌트만 존재 | ❌ 상세 UI에서 막힘 | `InterviewSection`, routes/services는 있으나 상세 page에 mount/import 없음 |
| 관리자 최종결정 | ⚠️ API/컴포넌트만 존재 | ❌ 상세 UI에서 막힘 | `HiringDecisionSection`, BFF/API는 있으나 상세 page에 mount/import 없음 |

## MVP Checklist

### 지원자 플로우

- [x] 공고 목록 조회/검색/필터
- [x] 공고 상세 조회
- [x] 로그인 필요 시 `/auth/login?next=...` 복귀
- [x] 프로필 작성/저장
- [x] 지원서 4-step 작성
- [x] 임시저장/기존 draft 복원
- [x] 제출 후 `/me?submitted=1` 완료 배너
- [x] 내 지원 목록/지원서 읽기
- [ ] 프로필 템플릿 전체를 지원서에 자연스럽게 반영
- [ ] 공고별 required custom question 제출 검증 강화

### 관리자 플로우

- [x] 공고 목록/등록/수정
- [x] 공고 질문 관리
- [x] 지원자 목록/공고/상태/검색 필터
- [x] 지원자 상세 읽기
- [x] 첨부파일 목록/다운로드 링크
- [ ] 지원자 상세에서 심사 상태 변경 UI 연결
- [ ] 지원자 상세에서 면접 등록/상태 변경/평가 UI 연결
- [ ] 지원자 상세에서 최종결정 UI 연결
- [ ] 위 3개 액션을 한 데모 시나리오에서 검증

## 데모에서 막힐 지점

1. `/admin/applicants/[id]` 상세 화면에 상태 변경 폼이 없다. 현재는 상태 뱃지와 메모 읽기만 가능하다.
2. 면접/평가 섹션이 화면에 연결되어 있지 않아 “상세 → 면접 등록 → 완료 → 평가”를 보여줄 수 없다.
3. 최종결정 섹션이 화면에 연결되어 있지 않아 “합격 → 처우 제안 → 수락/거절”을 관리자 UI로 마무리할 수 없다.
4. 프로필의 자기소개/핵심강점 템플릿은 저장되지만 지원서 Step2에 자동 import되지 않아 “프로필 반복 활용” 데모 메시지가 일부 약하다.

## 첫 구현 task 후보 3개

1. **P0 — AdminApplicantDetail에 기존 mutation 패널 연결**
   - `ApplicantReviewForm`, `InterviewSection`, `HiringDecisionSection` mount
   - `getAdminInterviews`, `getAdminJobPostingSteps` fetch 추가
   - 목표: 관리자 상세에서 상태변경/면접/최종결정이 실제 클릭 가능

2. **P1 — 지원자 프로필 import 완성**
   - 프로필의 `introductionTemplate`, `coreStrengthTemplate`, `careerYears`를 지원서 Step2에 반영
   - 현재 Step3 구조화 이력 import와 UX 통합
   - 목표: “프로필 선작성 → 지원서 작성 시간 단축” 메시지 완성

3. **P1 — MVP 데모 smoke 검증 추가**
   - README seed 기준 공고 `1001 / platform-backend-engineer`와 지원자/관리자 주요 루트 검증
   - 최소 수동 체크리스트 또는 Playwright smoke로 공고→지원→관리자 상세 mutation 루프 확인
   - 목표: 데모 직전 회귀 리스크 감소

## Done Definition

- [x] README만 보고 기본 실행 방법 파악 가능
- [x] demo seed data 위치 존재
- [x] 지원자 핵심 플로우 E2E 가능
- [ ] 관리자 화면에서 상태 변경 가능
- [ ] 관리자 화면에서 면접/평가 가능
- [ ] 관리자 화면에서 최종결정 가능
- [ ] seed 데이터로 5분 이내 데모 리허설 가능
