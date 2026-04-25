# OpenClaw Queue

## Rules

- 이 파일에 있는 작업만 수행한다.
- `approved: true`가 없는 작업은 코드 수정하지 않는다.
- 기본은 main/master 직접 push 금지. 단, 석이가 명시적으로 main/master 작업/push/merge를 승인하면 허용한다. 미반영 변경사항은 반드시 보고한다.
- 작업 전 plan 작성.
- 작업 후 Execution-Log에 결과 기록.

## Queue

- [ ] id: VIBE-GRID-001
  priority: P1
  mode: plan
  approved: false
  title: "README/docs 기반 현재 상태 요약"
  expected_output: "Project.md 현재 상태 갱신"

- [ ] id: VIBE-GRID-002
  priority: P2
  mode: plan
  approved: false
  title: "다음 완성 루프 정의"
  expected_output: "MVP/roadmap 문서 갱신"

- [ ] id: VIBE-GRID-001
  priority: P1
  mode: branch_pr
  approved: false
  title: "Public API와 테스트 현황 분석"
  expected_output: "Public-API.md, QA-Matrix.md 갱신"

- [ ] id: VIBE-GRID-002
  priority: P1
  mode: branch_pr
  approved: false
  title: "clipboard/excel/persistence 중 가장 약한 영역 하나를 테스트로 보강"
  expected_output: "테스트 추가, Execution-Log 기록"
