# OpenClaw Queue

## Rules

- 이 파일에 있는 작업만 수행한다.
- `approved: true`가 없는 작업은 코드 수정하지 않는다.
- 기본은 main/master 직접 push 금지. 단, 석이가 명시적으로 main/master 작업/push/merge를 승인하면 허용한다. 미반영 변경사항은 반드시 보고한다.
- 작업 전 plan 작성.
- 작업 후 Execution-Log에 결과 기록.

## Queue

- [x] id: VIBE-REC-001
  priority: P1
  mode: plan
  approved: false
  title: "README/docs 기반 현재 상태 요약"
  expected_output: "MVP-Scope.md 현재 상태 갱신"
  result: "2026-04-25 MVP gap 분석으로 완료"

- [x] id: VIBE-REC-002
  priority: P1
  mode: plan
  approved: false
  title: "지원자 플로우와 관리자 플로우의 MVP gap 분석"
  expected_output: "MVP-Scope.md, Demo-Scenario.md, Admin-Flow.md 갱신"
  result: "2026-04-25 문서 갱신 완료. 코드 수정 없음."

- [ ] id: VIBE-REC-003
  priority: P0
  mode: branch_pr
  approved: false
  title: "관리자 지원자 상세에 심사/면접/최종결정 패널 연결"
  expected_output: "`/admin/applicants/[id]`에서 상태변경, 면접 등록/평가, 최종결정 가능"
  notes:
    - "기존 컴포넌트: ApplicantReviewForm, InterviewSection, HiringDecisionSection"
    - "기존 API/BFF: review-status, interviews, evaluations, final-decision"
    - "필요 fetch: getAdminInterviews(applicationId), getAdminJobPostingSteps(applicant.jobPostingId)"
    - "데모 blocker 해소 1순위"

- [ ] id: VIBE-REC-004
  priority: P1
  mode: branch_pr
  approved: false
  title: "지원자 프로필 import를 지원서 Step2까지 확장"
  expected_output: "프로필의 자기소개/핵심강점/경력연수가 지원서 작성에 반영"
  notes:
    - "현재 Step3 이력/경력/스킬/자격/언어만 import"
    - "제품 메시지: 프로필 선작성으로 반복 입력 감소"

- [ ] id: VIBE-REC-005
  priority: P1
  mode: branch_pr
  approved: false
  title: "MVP demo smoke 체크리스트/검증 추가"
  expected_output: "seed 데이터 기준 공고→지원→관리자 운영 액션 smoke 검증"
  notes:
    - "README hotspot: 1001 / platform-backend-engineer"
    - "관리자 상세 mutation 연결 후 수행"
    - "수동 체크리스트 또는 최소 Playwright smoke 중 선택"

## Execution-Log

- 2026-04-25: VibeRec MVP gap 분석 수행. Obsidian 문서 5개 갱신. 코드 수정/커밋/push 없음.
