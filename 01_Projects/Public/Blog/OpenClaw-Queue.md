# OpenClaw Queue

## Rules

- 이 파일에 있는 작업만 수행한다.
- `approved: true`가 없는 작업은 코드 수정하지 않는다.
- 기본은 main/master 직접 push 금지. 단, 석이가 명시적으로 main/master 작업/push/merge를 승인하면 허용한다. 미반영 변경사항은 반드시 보고한다.
- 작업 전 plan 작성.
- 작업 후 Execution-Log에 결과 기록.
- 관찰/문서 갱신은 코드 수정이 아니므로 허용된다.

## Queue

- [ ] id: BLOG-OBS-001
  priority: P1
  mode: observe
  approved: true
  title: "GitHub Repo Deep Dive 첫 scheduled run 관찰"
  expected_time: "2026-04-28 07:10 KST 이후"
  expected_output: "Workflow-Status.md, Analyzed-Repos.md 갱신; 새 post/state/URL/Pages deploy 확인"
  checklist:
    - "GitHub Actions: Generate Star Repo Deep Dive run status"
    - "새 `_posts/YYYY-MM-DD-repo-deep-dive-*.md` 생성 여부"
    - "`.automation/star_repo_analysis.json` last_run_at/analyzed 변경"
    - "Published URL HTTP 200"
    - "Pages deploy success"

- [ ] id: BLOG-OBS-002
  priority: P2
  mode: observe
  approved: true
  title: "48시간 guard skip 동작 확인"
  expected_time: "2026-04-26 07:10 KST 또는 2026-04-27 07:10 KST 이후"
  expected_output: "Workflow-Status.md에 skip 여부 기록"
  note: "last_run_at=2026-04-25T21:13:31+09:00 기준 48시간 전에는 skip이 정상"

- [ ] id: BLOG-PLAN-003
  priority: P2
  mode: plan
  approved: false
  title: "giscus-comment-alert.yml push-time failure 원인 점검"
  expected_output: "원인/수정안 제시. 코드 수정은 별도 승인 필요"

- [x] id: BLOG-DOC-004
  priority: P1
  mode: observe
  approved: true
  title: "오늘 추가한 GitHub Repo Deep Dive 카테고리/첫 글/워크플로 상태 문서화"
  completed: "2026-04-26 KST"
  expected_output: "Blog.md, Analyzed-Repos.md, Workflow-Status.md, Weekly-Review.md, OpenClaw-Queue.md 갱신"
