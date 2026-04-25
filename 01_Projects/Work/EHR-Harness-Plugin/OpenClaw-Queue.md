# OpenClaw Queue

## Rules

- 이 파일에 있는 작업만 수행한다.
- `approved: true`가 없는 작업은 코드 수정하지 않는다.
- main/master 직접 push 금지.
- 작업 전 plan 작성.
- 작업 후 Execution-Log에 결과 기록.

## Queue

- [ ] id: EHR-HARNESS-001
  priority: P1
  mode: plan
  approved: false
  title: "README/docs 기반 현재 상태 요약"
  expected_output: "Project.md 현재 상태 갱신"

- [ ] id: EHR-HARNESS-002
  priority: P2
  mode: plan
  approved: false
  title: "다음 완성 루프 정의"
  expected_output: "MVP/roadmap 문서 갱신"

- [ ] id: EHR-HARNESS-001
  priority: P0
  mode: plan
  approved: false
  title: "현재 배포/수정 루프와 안전장치 점검"
  expected_output: "Release-Log.md, Plugin-Roadmap.md 갱신"
