# OpenClaw Prompt Library

이 문서는 개인 repo 운영체계를 반복 실행하기 위한 표준 프롬프트 모음이다.

핵심 원칙:

> OpenClaw가 알아서 아무거나 고치게 하지 말고, Obsidian의 `OpenClaw-Queue.md`에 있는 승인된 작업만 처리하게 만든다.

## 1. 매일 실행용 프롬프트

```markdown
내 repo 운영체계의 daily loop를 실행해.

대상 workspace:

```bash
BASE_DIR="$HOME/dev/qoxmfaktmxj"
```

해야 할 일:

1. 내가 언급한 모든 repo를 동기화한다.
   - repo가 없으면 clone.
   - repo가 있으면 fetch.
   - clean repo만 pull --ff-only.
   - dirty repo는 pull하지 말고 report에 기록.
   - reset/clean/delete/push 금지.

2. `kms_obsidian/08_Automation/openclaw/Repo-Sync-Report.md`를 갱신한다.

3. `kms_obsidian`의 active project note들을 읽는다.

4. 각 `OpenClaw-Queue.md`를 읽는다.

5. 오늘 집중할 작업 3개를 추천한다.

6. 추천 기준:
   - P0/P1 우선.
   - Jarvis는 다음주 업무 준비 우선.
   - EHR Harness Plugin은 배포/피드백/안전성 우선.
   - VibeGrid는 테스트와 Public API 안정화 우선.
   - VibeRec은 SaaS 데모 완성 우선.
   - VibeHR은 cycle 단위 설계 우선.
   - TripCart는 낮은 우선순위.
   - Blog는 star repo deep-dive 자동화 상태 확인.

7. 코드 수정은 하지 마라.

8. 결과를 한국어로 보고해.

출력 형식:
# Daily Repo Operating Report

## 1. Sync 결과

## 2. 오늘 집중 후보 3개

## 3. 승인 필요한 작업

## 4. 내가 직접 해야 할 일

## 5. OpenClaw가 다음에 실행 가능한 명령
```

## 2. 특정 repo 분석용 프롬프트

예: `vibe-grid` repo snapshot.

```markdown
`vibe-grid` repo snapshot을 만들어줘.

workspace:

```bash
BASE_DIR="$HOME/dev/qoxmfaktmxj"
```

대상 repo:
https://github.com/qoxmfaktmxj/vibe-grid

해야 할 일:

1. repo가 없으면 clone.
2. 있으면 fetch.
3. clean이면 pull --ff-only.
4. dirty이면 pull하지 말고 fetch만 한다.
5. README, docs, package config, test config, workflow를 읽는다.
6. 추측하지 말고 실제 파일 근거로만 현재 상태를 정리한다.
7. `kms_obsidian/01_Projects/Products/VibeGrid/VibeGrid.md`를 갱신한다.
8. Public-API.md, QA-Matrix.md, `OpenClaw-Queue.md`를 갱신한다.
9. 코드 수정은 하지 않는다.
10. 다음에 branch_pr로 실행할 만한 task 3개를 제안한다.

출력:
# VibeGrid Snapshot

## 1. 현재 상태

## 2. 작동하는 것

## 3. 미완성인 것

## 4. 위험한 것

## 5. 다음 작업 후보 3개

## 6. 수정한 Obsidian 파일
```

## 3. 승인된 task 실행용 프롬프트

실제 코드 수정용. `approved: true`로 바꾼 task에만 사용한다.

```markdown
승인된 OpenClaw task를 실행해.

workspace:

```bash
BASE_DIR="$HOME/dev/qoxmfaktmxj"
```

project:
<프로젝트명>

task id:
<TASK_ID>

규칙:

1. `kms_obsidian`의 해당 프로젝트 `OpenClaw-Queue.md`에서 task를 찾는다.
2. task에 `approved: true`가 없으면 중단한다.
3. 해당 repo의 `openclaw_mode`가 `branch_pr`이 아니면 중단한다.
4. 기본은 main/master에서 직접 수정하지 않는다. 단, 석이가 명시적으로 main/master 작업을 승인하면 허용한다.
5. 작업 branch를 만든다.

branch 이름:
openclaw/<task_id-kebab-case>

6. 작업 전 plan을 작성한다.
7. plan에는 영향 파일, 구현 전략, 테스트 전략을 포함한다.
8. 구현한다.
9. 가능한 테스트를 실행한다.
10. 실패하면 실패 내용을 기록하고 멈춘다.
11. 성공하면 diff summary를 작성한다.
12. 기본은 push하지 않는다. 단, 석이가 명시적으로 push/merge까지 승인하면 수행할 수 있다.
13. `kms_obsidian/08_Automation/openclaw/Execution-Log.md`에 결과를 기록한다.
14. 해당 Project Note와 Weekly-Review를 갱신한다.

금지:
- git reset --hard
- git clean -fd
- rm -rf
- git push (단, 석이 명시 승인 시 허용)

출력:
# Task Execution Report

## 1. Task

## 2. Branch

## 3. 변경 파일

## 4. 구현 내용

## 5. 테스트 결과

## 6. 남은 위험

## 7. push하려면 실행할 명령
```

## 4. GitHub star 50,000+ repo 블로그 자동화 전용 프롬프트

```markdown
`qoxmfaktmxj.github.io` repo에 GitHub star 50000+ repo deep-dive 자동화를 구현해.

workspace:

```bash
BASE_DIR="$HOME/dev/qoxmfaktmxj"
```

대상 repo:
https://github.com/qoxmfaktmxj/qoxmfaktmxj.github.io

동기화 규칙:

1. repo가 없으면 clone.
2. 있으면 fetch.
3. clean이면 pull --ff-only.
4. dirty이면 pull하지 않고 중단 보고.
5. 기본은 main/master 직접 수정 금지. 단, 석이가 명시 승인하면 가능.
6. branch 생성:
   chore/star-repo-deep-dive-automation-$(date +%Y%m%d)

구현할 파일:
- scripts/star_repo_deep_dive.py
- .automation/star_repo_analysis.json
- .github/workflows/star-repo-deep-dive.yml

자동화 요구사항:

1. GitHub API로 star 50000 이상 repo 검색.
2. query: `stars:>50000 fork:false archived:false`
3. sort stars desc.
4. 이미 분석한 repo는 제외.
5. state file에 analyzed repo 기록.
6. 48시간 이내 중복 실행 방지.
7. 후보가 없으면 exhausted true.
8. `_posts`에 markdown 생성.
9. 포스트는 상세 분석 구조를 가진다.
10. backend developer 관점에서 배울 점을 포함한다.
11. 내 프로젝트에 적용할 아이디어를 반드시 포함한다.
    - vibe-grid
    - vibe-hr
    - vibe-rec
    - jarvis
    - ehr-harness-plugin
    - tripcart
12. 기본은 push하지 않는다. 단, 석이가 명시적으로 push/merge까지 승인하면 수행할 수 있다.
13. commit까지만 한다.
14. 최종 보고서에 push 명령을 제안한다.

포스트 템플릿:

---
layout: post
title: "Repo Deep Dive: owner/repo"
date: YYYY-MM-DD HH:mm:ss +0900
categories: [github-repo-analysis]
tags: [github, architecture, backend, open-source, deep-dive]
repo: owner/repo
stars: 00000
analyzed_at: YYYY-MM-DD
---

## 1. 이 repo가 중요한 이유

## 2. 한 문장 요약

## 3. 제품/문제 정의

## 4. 아키텍처 구조

## 5. 핵심 모듈

## 6. 백엔드 개발자가 배울 점

## 7. 내 프로젝트에 훔쳐올 패턴

## 8. 주의할 점 / 안티패턴

## 9. vibe-grid / vibe-hr / jarvis / ehr-harness에 적용할 아이디어

## 10. Source Links

최종 출력:
# Star Repo Deep Dive Automation Report

## 1. 생성 파일

## 2. 동작 방식

## 3. state 관리 방식

## 4. GitHub Actions 동작 방식

## 5. 테스트 결과

## 6. push 명령
```

## 5. LLM Wiki 갱신 전용 프롬프트

```markdown
내 Obsidian LLM Wiki를 갱신해.

workspace:

```bash
BASE_DIR="$HOME/dev/qoxmfaktmxj"
```

대상:
- kms_obsidian
- ehr-harness-plugin
- jarvis
- vibe-grid
- vibe-hr
- vibe-rec
- tripcart
- qoxmfaktmxj.github.io
- landing-minseok91

해야 할 일:

1. 모든 repo를 최신 동기화한다.
2. dirty repo는 pull하지 않는다.
3. 각 repo의 README/docs/config를 읽는다.
4. `kms_obsidian/07_LLM_Wiki`를 갱신한다.
5. raw 자료를 그대로 복붙하지 않는다.
6. 편집된 concept page로 정리한다.
7. 불확실한 내용은 `confidence: low`로 표시한다.
8. 모순 가능성은 `07_LLM_Wiki/_system/contradictions.md`에 기록한다.
9. 오래된 페이지는 `07_LLM_Wiki/_system/stale-pages.md`에 기록한다.
10. 코드 수정은 하지 않는다.

갱신 대상 concept:
- HR-EHR-AI-Agent-System
- LLM-Wiki-Operating-Model
- VibeGrid-Platform
- VibeHR-Domain
- Recruiting-SaaS
- GitHub-Repo-Deep-Dive-Lessons

출력:
# LLM Wiki Update Report

## 1. 갱신한 페이지

## 2. 새로 발견한 연결

## 3. 모순 가능성

## 4. stale page

## 5. 다음에 분석할 주제
```

## 6. 주간 리뷰용 프롬프트

```markdown
이번 주 repo 운영 weekly review를 작성해.

workspace:

```bash
BASE_DIR="$HOME/dev/qoxmfaktmxj"
```

해야 할 일:

1. 모든 repo를 동기화한다.
2. 각 project note를 읽는다.
3. 각 OpenClaw-Queue를 읽는다.
4. 이번 주 변경사항을 repo별로 확인한다.
5. 각 프로젝트의 `Weekly-Review.md`를 갱신한다.
6. 다음 주 P1 task를 repo별로 1개 이하로 정한다.
7. 너무 많은 task를 만들지 마라.
8. 미완성 루프를 명확히 적는다.
9. 코드 수정은 하지 않는다.

프로젝트별 전략:

- Jarvis: 다음주 업무 sprint 중심.
- EHR Harness Plugin: 배포/수정/피드백 중심.
- VibeGrid: 테스트와 public API 안정화.
- VibeRec: 완성본에 가까운 SaaS 데모.
- VibeHR: cycle 단위 완성.
- TripCart: 보류/아이디어 보존.
- Blog: star repo deep-dive 자동화.
- Landing: 유지.

출력:
# Weekly Operating Review

## 1. 전체 요약

## 2. repo별 진전

## 3. 막힌 것

## 4. 다음 주 P1

## 5. OpenClaw에게 맡길 것

## 6. 내가 직접 해야 할 것
```

## 7. 추천 실제 실행 순서

```text
1. 최초 1회 실행용 마스터 프롬프트 실행
2. 결과 확인
3. kms_obsidian 변경 branch push
4. qoxmfaktmxj.github.io 변경 branch push
5. GitHub에서 PR 확인
6. 이후 매일 “매일 실행용 프롬프트” 실행
7. 주 1회 “주간 리뷰용 프롬프트” 실행
```

처음부터 코드 자동수정까지 열지 않는다.
첫 목표는 **OpenClaw가 볼 수 있는 질서 있는 작업 큐와 문서 체계**를 만드는 것이다.

권장 초기 권한:

| Repo | Mode |
|---|---|
| kms_obsidian | branch_pr |
| jarvis | plan_only |
| ehr-harness-plugin | plan_only |
| vibe-grid | branch_pr |
| vibe-hr | plan_only |
| vibe-rec | branch_pr |
| tripcart | branch_pr |
| qoxmfaktmxj.github.io | branch_pr |
| landing-minseok91 | read_only |


## 8. Main/Master 명시 승인 운영 원칙

기본값은 branch 기반 안전 작업이다.
하지만 석이가 명시하면 OpenClaw는 main/master 직접 작업, push, merge까지 수행할 수 있다.

필수 조건:

1. 석이의 명시 승인이 있어야 한다.
2. 작업 전 현재 branch, dirty 상태, upstream 상태를 확인한다.
3. 작업 후 테스트 또는 최소 검증을 수행한다.
4. main/master에 반영되지 않은 변경사항이 있으면 최종 보고에 반드시 포함한다.
5. 보고에는 repo, branch, commit, 남은 조치, 실행할 push/merge 명령을 포함한다.
6. secret 출력, destructive command, production data write 금지는 유지한다.

보고 예시:

```markdown
## Main 반영 상태

- repo: qoxmfaktmxj.github.io
- branch: chore/star-repo-deep-dive-automation-20260425
- main 반영 여부: 미반영
- 필요한 조치: push 후 PR merge 또는 명시 승인 시 main merge
- 명령:
  git push -u origin chore/star-repo-deep-dive-automation-20260425
```
