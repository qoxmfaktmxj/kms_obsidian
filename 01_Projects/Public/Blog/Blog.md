---
type: project
status: active
lane: public
repo: https://github.com/qoxmfaktmxj/qoxmfaktmxj.github.io
local_path: ~/dev/qoxmfaktmxj/qoxmfaktmxj.github.io
maturity: usable
priority: P1
openclaw_mode: branch_pr_default_main_allowed_when_explicitly_approved
cadence: daily_posts_plus_48h_repo_deep_dive
last_reviewed: 2026-04-26
next_action: "2026-04-28 07:10 KST 이후 GitHub Repo Deep Dive scheduled run 관찰"
tags: [project, blog, writing, github-analysis, automation]
---

# Blog

## 1. 한 문장 정의

Jekyll 기반 공개 기술 블로그. AI Daily News/개발 학습 글과 별도로, GitHub star 50,000+ repo를 48시간 cadence로 분석하는 `GitHub Repo Deep Dive` 카테고리를 운영한다.

## 2. 현재 상태

- Local path: `~/dev/qoxmfaktmxj/qoxmfaktmxj.github.io`
- Remote: `origin/main`
- Branch: `main`
- HEAD: `fcabb72f post: add first git repo deep dive`
- Dirty: `no` at observation time
- Published root: `https://qoxmfaktmxj.github.io/` → HTTP 200 확인
- First deep-dive URL: `https://qoxmfaktmxj.github.io/github-repo-analysis/2026/04/25/repo-deep-dive-codecrafters-io-build-your-own-x.html` → HTTP 200 확인

### 작동하는 것

- GitHub Pages deploy for `fcabb72f` succeeded.
  - Run: `https://github.com/qoxmfaktmxj/qoxmfaktmxj.github.io/actions/runs/24930660339`
  - Created: `2026-04-25T12:14:38Z`
  - Updated: `2026-04-25T12:15:19Z`
- 새 카테고리 `github-repo-analysis`가 첫 글과 홈페이지 HTML에 노출됨.
- 첫 글: `_posts/2026-04-25-repo-deep-dive-codecrafters-io-build-your-own-x.md`
- State file `.automation/star_repo_analysis.json`에 분석 완료 repo가 기록됨.
- `python3 scripts/star_repo_deep_dive.py --dry-run`은 48시간 guard로 정상 skip.

### 미완성/관찰 필요

- `Generate Star Repo Deep Dive` workflow는 아직 GitHub Actions run 이력이 없음(`total_count 0`). 첫 schedule 도달 전 상태로 보임.
- 48시간 guard 기준 다음 자동 생성 가능 시점은 `2026-04-27 21:13:31 KST` 이후다.
- 실제 cron은 매일 `22:10 UTC` = `07:10 KST`에 실행되므로, 다음 생성 예상 관찰 시점은 `2026-04-28 07:10 KST` 이후다.
- `giscus-comment-alert.yml`은 최근 push마다 failure check가 보임. Pages/deep-dive와는 별도 알림 workflow지만, 빨간 체크가 거슬리면 별도 점검 대상.

### 위험한 것

- `star-repo-deep-dive.yml`은 `contents: write` 권한으로 `_posts`와 `.automation`을 커밋/push한다. 의도된 동작이지만 main 직접 변경이므로 run 결과 관찰 필요.
- 새 workflow는 `workflow_run`으로 Pages deploy를 직접 부르지는 않는다. 대신 main push trigger로 Pages deploy가 실행되는 구조다.
- secrets 값은 열람/출력하지 않음. workflow는 `GITHUB_TOKEN`, `ANTHROPIC_API_KEY`, `OPENAI_API_KEY` 존재 여부에 따라 동작한다.

## 3. 자동화 구성 요약

| 구분 | 파일 | 실행 | 생성물 | 상태 파일 | 비고 |
|---|---|---|---|---|---|
| 일반 자동 글 | `.github/workflows/auto-post.yml` | 현재 YAML 기준 `workflow_dispatch` only | AI Daily News + study post | `.automation/state.json` | `scripts/auto_post.py` |
| GitHub Repo Deep Dive | `.github/workflows/star-repo-deep-dive.yml` | `workflow_dispatch` + daily cron `22:10 UTC` | `github-repo-analysis` post | `.automation/star_repo_analysis.json` | `scripts/star_repo_deep_dive.py`, 48h guard |
| Pages deploy | `.github/workflows/pages-deploy.yml` | main push + manual + legacy auto-post workflow_run | GitHub Pages | n/a | latest `fcabb72f` success |

## 4. 이번 주 목표

- [x] GitHub Repo Deep Dive 카테고리/첫 글 발행 확인
- [x] Pages deploy 성공 확인
- [x] 일반 auto-post와 deep-dive workflow 분리 확인
- [ ] 첫 scheduled deep-dive run 결과 확인

## 5. OpenClaw 작업 큐

> OpenClaw는 이 섹션 또는 별도 `OpenClaw-Queue.md`에 있는 일만 수행한다.

- [ ] #openclaw mode:observe priority:P1 `2026-04-28 07:10 KST` 이후 `Generate Star Repo Deep Dive` 첫 scheduled run, state, 새 post 여부 확인
- [ ] #openclaw mode:plan priority:P2 `giscus-comment-alert.yml` push-time failure 원인 분리 점검

## 6. 결정사항

| 날짜 | 결정 | 이유 | 되돌릴 조건 |
|---|---|---|---|
| 2026-04-25 | 개인 개발 운영체제 관리 대상에 등록 | 공유대화/운영 프롬프트 기준 | repo 운영 대상에서 제외될 때 |
| 2026-04-25 | `github-repo-analysis` 카테고리 신설 | GitHub 50k+ star repo deep dive를 기존 daily/news와 분리 | 카테고리 운영 중단 시 |
| 2026-04-25 | deep-dive 자동화는 기존 `auto_post.py`와 분리 | cadence/state/콘텐츠 목적이 다름 | 하나의 editorial pipeline으로 통합 결정 시 |

## 7. 배운 것 / 인사이트

- Deep-dive cadence는 workflow cron이 아니라 script state guard가 최종 제어한다.
- 첫 글 수동 게시 후 state가 이미 기록되어 있어, 첫 scheduled run은 48시간 이내면 정상 skip해야 한다.
- Pages deploy는 새 workflow를 몰라도 main push만 성공하면 배포된다.

## 8. 관련 문서

- [[Analyzed-Repos]]
- [[Workflow-Status]]
- [[OpenClaw-Queue]]
- [[Weekly-Review]]
- [[Decisions]]
- [[Star-Repo-Deep-Dive-Automation]]

## 9. 확인된 근거

- `git status --short --branch`: `## main...origin/main`
- `git log -n 1`: `fcabb72f post: add first git repo deep dive`
- `.automation/star_repo_analysis.json`: `last_run_at=2026-04-25T21:13:31+09:00`, `analyzed=[codecrafters-io/build-your-own-x]`
- Published URL HTTP 200 and title/category/repo string present.
