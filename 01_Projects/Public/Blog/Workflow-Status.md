# Workflow Status - Blog

Observed at: `2026-04-25 15:21-15:35 UTC` / `2026-04-26 00:21-00:35 KST`

## Summary

| Workflow | File | Current trigger | Recent status | Notes |
|---|---|---|---|---|
| Generate Star Repo Deep Dive | `.github/workflows/star-repo-deep-dive.yml` | manual + daily `22:10 UTC` | no runs yet (`total_count 0`) | Script-level 48h guard controls actual generation |
| Manual Generate Posts | `.github/workflows/auto-post.yml` | manual only in current YAML | no recent current runs observed; API has older scheduled history | Existing AI Daily News/study pipeline |
| Deploy Jekyll site to Pages | `.github/workflows/pages-deploy.yml` | main push + manual + legacy auto-post workflow_run | success for `fcabb72f` | Published first deep-dive post |
| Giscus Comment Alert | `.github/workflows/giscus-comment-alert.yml` | discussion_comment | failure checks appeared on recent pushes | Unrelated to Pages/deep-dive; separate follow-up if needed |

## Latest Pages deploy

- Commit: `fcabb72f post: add first git repo deep dive`
- Status: `completed / success`
- Created: `2026-04-25T12:14:38Z`
- Updated: `2026-04-25T12:15:19Z`
- Run: `https://github.com/qoxmfaktmxj/qoxmfaktmxj.github.io/actions/runs/24930660339`

## Published URL checks

- `https://qoxmfaktmxj.github.io/` → HTTP 200; contains `Repo Deep Dive: codecrafters-io/build-your-own-x`, `github-repo-analysis`.
- `https://qoxmfaktmxj.github.io/github-repo-analysis/2026/04/25/repo-deep-dive-codecrafters-io-build-your-own-x.html` → HTTP 200; title is `Repo Deep Dive: codecrafters-io/build-your-own-x | 석이's Blog`.

## Deep-dive workflow contract observed

- Workflow file: `.github/workflows/star-repo-deep-dive.yml`
- Script: `scripts/star_repo_deep_dive.py`
- State: `.automation/star_repo_analysis.json`
- Commit scope in workflow: `git add _posts .automation`
- Permissions: `contents: write`
- Concurrency group: `star-repo-deep-dive`
- Checkout ref: `main`

## Separation from existing auto-post

Confirmed separated.

- Deep-dive uses separate workflow file, script, state file, category, cadence, and commit message.
- Existing auto-post uses `scripts/auto_post.py` and `.automation/state.json` for AI Daily News/study posts.
- Deep-dive state file does not overlap with daily post state.
- Pages deploy does not explicitly list the new workflow under `workflow_run`, but main push trigger covers deploy after deep-dive workflow commits.

## Next observation

- `2026-04-26 07:10 KST`: first cron after creation may run, but should skip because within 48h.
- `2026-04-27 07:10 KST`: still within 48h from `2026-04-25 21:13 KST`, should skip.
- `2026-04-28 07:10 KST`: first scheduled run expected to be eligible to create the next deep-dive post.
