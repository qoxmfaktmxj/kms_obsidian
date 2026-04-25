# OpenClaw Queue

## Rules

- 이 파일에 있는 작업만 수행한다.
- `approved: true`가 없는 작업은 코드 수정하지 않는다.
- 기본은 main/master 직접 push 금지. 단, 석이가 명시적으로 main/master 작업/push/merge를 승인하면 허용한다. 미반영 변경사항은 반드시 보고한다.
- 작업 전 plan 작성.
- 작업 후 Execution-Log에 결과 기록.

## Queue

- [ ] id: VIBE-REC-001
  priority: P1
  mode: plan
  approved: false
  title: "README/docs 기반 현재 상태 요약"
  expected_output: "Project.md 현재 상태 갱신"

- [ ] id: VIBE-REC-002
  priority: P2
  mode: plan
  approved: false
  title: "다음 완성 루프 정의"
  expected_output: "MVP/roadmap 문서 갱신"

- [ ] id: VIBE-REC-001
  priority: P1
  mode: branch_pr
  approved: false
  title: "지원자 플로우와 관리자 플로우의 MVP gap 분석"
  expected_output: "MVP-Scope.md, Demo-Scenario.md 갱신"

- [ ] id: VIBE-REC-002
  priority: P1
  mode: branch_pr
  approved: false
  title: "완성본에 가까운 SaaS 데모를 위한 첫 구현 task 제안"
  expected_output: "OpenClaw-Queue.md에 세부 task 3개 추가"
