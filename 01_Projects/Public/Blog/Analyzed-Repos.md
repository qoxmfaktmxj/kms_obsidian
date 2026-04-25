# Analyzed-Repos

## GitHub Repo Deep Dive 분석 이력

| 분석일(KST) | Repo | Stars at post | Post | State 반영 | 비고 |
|---|---|---:|---|---|---|
| 2026-04-25 | `codecrafters-io/build-your-own-x` | 495,421 | `https://qoxmfaktmxj.github.io/github-repo-analysis/2026/04/25/repo-deep-dive-codecrafters-io-build-your-own-x.html` | yes | 첫 `github-repo-analysis` 글 |

## 현재 state snapshot

Source: `~/dev/qoxmfaktmxj/qoxmfaktmxj.github.io/.automation/star_repo_analysis.json`

```json
{
  "min_stars": 50000,
  "last_run_at": "2026-04-25T21:13:31+09:00",
  "analyzed": [
    "codecrafters-io/build-your-own-x"
  ],
  "exhausted": false,
  "last_candidate_refresh": "2026-04-25T21:13:34+09:00"
}
```

## 다음 후보 선택 규칙

- Query: `stars:>50000 fork:false archived:false`
- Sort: stars desc
- 이미 `analyzed`에 있는 repo는 제외
- 후보 없음: `exhausted=true`
- 48시간 이내 재실행: post/state 변경 없이 skip

## 관찰 포인트

- 다음 실제 생성 예상: `2026-04-28 07:10 KST` scheduled run 이후
- 다음 글이 생성되면 이 표에 repo/post URL/state 변경을 추가한다.
