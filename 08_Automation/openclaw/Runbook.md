# OpenClaw Runbook

## Daily Loop

1. `/kms:sync-repos`
2. `/kms:today`
3. 가장 중요한 task 1개 선택
4. `/kms:plan {project} {task_id}`
5. 사람이 승인하면 `/kms:execute {project} {task_id}`
6. 결과를 Execution-Log에 기록
7. Project Note와 LLM Wiki 갱신

## Weekly Loop

1. 모든 active project Weekly-Review.md 갱신
2. stale task 정리
3. priority 재조정
4. 다음 주 P1 task 선정
5. 블로그 deep-dive 결과를 LLM Wiki로 흡수

## Incident Rule

문제가 생기면 다음을 우선한다.

1. 실행 중단
2. 현재 branch와 diff 기록
3. Incident-Log.md 기록
4. 사람에게 보고
