# OpenClaw Command Catalog

## /kms:sync-repos

목표:
- 모든 repo를 clone/fetch/pull 한다.
- dirty repo는 pull하지 않고 fetch만 한다.
- 결과를 Repo-Sync-Report.md에 기록한다.

권한:
- read_only
- clean repo에 한해 pull 허용
- push 금지

---

## /kms:today

읽기:
- 06_Daily 오늘 노트
- active project notes
- 각 OpenClaw-Queue.md

출력:
- 오늘 집중 3개
- 미룰 것
- 승인 필요한 작업

권한:
- read_only

---

## /kms:repo-snapshot {repo}

읽기:
- README
- docs
- build config
- workflow
- 최근 commit

쓰기:
- 해당 Project.md
- Weekly-Review.md

권한:
- read_only

---

## /kms:plan {project} {task_id}

읽기:
- Project.md
- OpenClaw-Queue.md
- repo code

쓰기:
- plan section only
- 코드 수정 금지

권한:
- plan_only

---

## /kms:execute {project} {task_id}

조건:
- task에 approved: true 필요
- repo mode가 branch_pr이어야 함

작업:
- branch 생성
- 코드 수정
- 테스트 실행
- diff summary 작성

쓰기:
- repo branch
- Execution-Log.md

금지:
- main/master push
- production secret 접근
- DB write

권한:
- branch_pr

---

## /kms:wiki-lint

읽기:
- 07_LLM_Wiki
- 01_Projects

출력:
- broken link
- stale page
- orphan page
- contradiction 후보

쓰기:
- 07_LLM_Wiki/_system/lint-reports
- 07_LLM_Wiki/_system/contradictions.md
- 07_LLM_Wiki/_system/stale-pages.md

권한:
- read_only + report write

---

## /kms:blog-star-repo

읽기:
- qoxmfaktmxj.github.io
- .automation/star_repo_analysis.json
- GitHub API

쓰기:
- _posts
- .automation/star_repo_analysis.json
- Obsidian GitHub-Repo-Deep-Dives note

조건:
- 이미 분석한 repo는 제외
- star 50000 이상
- 남은 후보가 없으면 중단

권한:
- branch_pr

## Prompt Library

- [[08_Automation/openclaw/Prompt-Library]]
