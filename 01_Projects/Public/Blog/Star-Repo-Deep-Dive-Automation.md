# Star-Repo-Deep-Dive-Automation

- 확인 필요

## 2026-04-25 구현 결과

- Blog repo branch: `chore/star-repo-deep-dive-automation-20260425`
- Commit: `9df93199 chore: add star repo deep dive automation`
- Added files:
  - `.automation/star_repo_analysis.json`
  - `scripts/star_repo_deep_dive.py`
  - `.github/workflows/star-repo-deep-dive.yml`
- Validation:
  - `python3 -m py_compile scripts/star_repo_deep_dive.py`: passed
  - `python3 scripts/star_repo_deep_dive.py --dry-run --force --min-stars 50000`: passed
- Dry-run candidate:
  - `codecrafters-io/build-your-own-x`

## 운영 방식

- GitHub Actions가 main에 직접 push하지 않고 `peter-evans/create-pull-request`로 PR branch를 만든다.
- script는 `.automation/star_repo_analysis.json`으로 2일 cadence와 analyzed repo 목록을 관리한다.
- 이미 분석한 repo는 frontmatter `source_repo`와 state 파일 기준으로 제외한다.

## 2026-04-25 요구사항 정합화

- Blog repo commit: `7709b306 chore: align star repo automation contract`
- State schema를 요청 형식으로 변경:
  - `min_stars`
  - `last_run_at`
  - `analyzed`
  - `exhausted`
  - `last_candidate_refresh`
- GitHub query를 `stars:>50000 fork:false archived:false` + stars desc로 변경.
- Post filename을 `_posts/YYYY-MM-DD-repo-deep-dive-owner-repo.md` 형식으로 변경.
- Frontmatter를 `github-repo-analysis` category와 `repo/stars/analyzed_at` 필드로 변경.
- GitHub Actions workflow를 요청한 `Generate Star Repo Deep Dive` 구조로 변경.
- Validation:
  - `python3 -m py_compile scripts/star_repo_deep_dive.py`: passed
  - `python3 scripts/star_repo_deep_dive.py --dry-run --force`: passed
