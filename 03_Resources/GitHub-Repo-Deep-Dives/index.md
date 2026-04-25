# GitHub Repo Deep Dives

이 공간은 GitHub star 50000+ repo 분석 결과를 모으고, 내 프로젝트에 적용할 수 있는 패턴으로 재가공하는 곳이다.

## 원칙

1. 이미 분석한 repo는 중복 분석하지 않는다.
2. 단순 소개글이 아니라 architecture, backend lesson, 적용 아이디어를 남긴다.
3. 매 분석글은 다음 프로젝트 중 어디에 적용할 수 있는지 연결한다.
   - VibeGrid
   - VibeHR
   - VibeRec
   - Jarvis
   - EHR Harness Plugin
   - TripCart

## 분석 목록

```dataview
TABLE repo, stars, analyzed_at, applicable_projects
FROM "03_Resources/GitHub-Repo-Deep-Dives"
WHERE type = "repo-deep-dive"
SORT analyzed_at DESC
```

## 운영 메모

- Blog workflow cron은 UTC 기준이다.
- `10 22 * * *`는 한국시간 오전 7시 10분 근처 실행 의도다.
- workflow는 매일 실행하되, 실제 2일 간격 판단은 `qoxmfaktmxj.github.io/scripts/star_repo_deep_dive.py`가 state 파일의 `last_run_at`으로 처리한다.
- 분석 결과가 생성되면 이 폴더에 Obsidian용 요약/패턴 추출 문서를 추가한다.
