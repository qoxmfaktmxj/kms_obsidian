# Admin-Flow

_Last updated: 2026-04-25 UTC_

## 현재 구현 요약

관리자 플로우는 **목록/상세 읽기와 공고 관리까지는 구현됨**. 하지만 MVP 운영 데모에 필요한 **상태변경/면접/최종결정 액션은 API와 컴포넌트만 있고 상세 화면에 연결되지 않았다.**

## Route Map

| 화면/API | 구현 상태 | 근거 |
|---|---:|---|
| `/admin` 공고 관리 대시보드 | ✅ | `apps/web/src/app/admin/(protected)/page.tsx` |
| `/admin/job-postings/new` 공고 등록 | ✅ | `JobPostingEditorForm`, `AdminJobPostingService.createJobPosting` |
| `/admin/job-postings/{id}` 공고 수정 | ✅ | `JobPostingEditorForm`, `AdminJobPostingService.updateJobPosting` |
| `/admin/job-postings/{id}/questions` 문항 관리 | ✅ | `JobPostingQuestionEditor`, `PUT /admin/job-postings/{id}/questions` |
| `/admin/applicants` 지원자 목록/필터 | ✅ | `AdminApplicantTable`, `AdminApplicantService.getApplicantsPage` |
| `/admin/applicants/{id}` 지원자 상세 읽기 | ✅ | `AdminApplicantDetailPage`, `AdminApplicantService.getApplicant` |
| `/api/admin/applicants/{id}/review-status` | ✅ | BFF route + `AdminApplicantService.updateReviewStatus` |
| `/api/admin/applicants/{id}/interviews` | ✅ | BFF route + `AdminInterviewService.createInterview/getInterviews` |
| `/api/admin/applicants/{id}/interviews/{interviewId}/status` | ✅ | BFF route + `AdminInterviewService.updateInterview` |
| `/api/admin/applicants/{id}/interviews/{interviewId}/evaluations` | ✅ | BFF route + `AdminInterviewService.createEvaluation` |
| `/api/admin/applicants/{id}/final-decision` | ✅ | BFF route + `AdminHiringDecisionService.makeFinalDecision` |

## 상세 화면 Gap

`apps/web/src/app/admin/applicants/[id]/page.tsx` 현재 import/렌더 범위:

- `getAdminApplicant`
- `getAdminAttachments`
- 상태 뱃지 표시
- 지원 메모/이력서/원본 JSON/첨부파일 표시

현재 연결되지 않은 컴포넌트:

- `apps/web/src/features/admin/applicants/ApplicantReviewForm.tsx`
- `apps/web/src/features/admin/interview/InterviewSection.tsx`
- `apps/web/src/features/admin/hiring/HiringDecisionSection.tsx`

따라서 관리자 상세는 “운영 콘솔”이 아니라 아직 “읽기 전용 상세”에 가깝다.

## Backend Business Rules 확인

| 기능 | 규칙 | 근거 |
|---|---|---|
| 심사 상태 변경 | 제출 완료 지원서만 상태 변경 가능. `NEW`로 되돌리기 금지. `NEW → IN_REVIEW → PASSED/REJECTED` 순서 요구 | `AdminApplicantService.validateReviewTransition` |
| 면접 등록 | 제출 완료 지원서만 면접 등록 가능. 같은 지원서/전형 단계 중복 면접 금지 | `AdminInterviewService.createInterview` |
| 평가 등록 | 완료된 면접만 평가 가능. 같은 면접/평가자 중복 평가 금지 | `AdminInterviewService.createEvaluation` |
| 최종결정 | `PASSED` 지원서만 `OFFER_MADE`, 이후 `ACCEPTED/DECLINED` 가능 | `AdminHiringDecisionService.validateFinalStatusTransition` |

## 관리자 MVP Action Plan

### 1. 지원자 상세에 심사 폼 연결

- `AdminApplicantDetailPage`에서 `ApplicantReviewForm` import/mount
- 상세 우측 또는 상단 summary 아래에 배치
- 성공 시 기존 컴포넌트의 `router.refresh()` 활용

### 2. 면접 섹션 연결

- `getAdminInterviews(applicationId)` fetch
- `getAdminJobPostingSteps(applicant.jobPostingId)` fetch
- `InterviewSection`에 `applicationId`, `interviews`, `steps` 전달
- 데모 경로: 면접 추가 → 완료 처리 → 평가 저장

### 3. 최종결정 섹션 연결

- `HiringDecisionSection`에 현재 `finalStatus/finalNote/finalDecidedAt/reviewStatus` 전달
- UX상 `reviewStatus === PASSED` 전에는 disabled 안내 유지
- 데모 경로: `PASSED` 후 `OFFER_MADE → ACCEPTED` 저장

## 데모 완료 기준

- [ ] 지원자 상세에서 상태 변경 버튼/폼이 보인다.
- [ ] `NEW → IN_REVIEW → PASSED` 변경 후 화면이 갱신된다.
- [ ] `PASSED` 상태에서 면접 추가 가능하다.
- [ ] 면접 `SCHEDULED → COMPLETED` 후 평가 저장 가능하다.
- [ ] 최종결정 `OFFER_MADE` 저장 가능하다.
- [ ] `ACCEPTED` 또는 `DECLINED` 저장 가능하다.
