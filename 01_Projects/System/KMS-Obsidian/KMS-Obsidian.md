---
type: project
status: active
lane: system
repo: https://github.com/qoxmfaktmxj/kms_obsidian
local_path: ~/dev/qoxmfaktmxj/kms_obsidian
maturity: prototype
priority: P0
openclaw_mode: branch_pr
cadence: daily
last_reviewed: 2026-04-25
next_action: "Repo 운영 대시보드와 LLM Wiki 구조 안정화"
tags: [project, obsidian, kms, control-plane]
---

# KMS-Obsidian

## 1. 한 문장 정의

개인 개발 운영체제 / Obsidian control plane.

## 2. 현재 상태

- Local path: `~/dev/qoxmfaktmxj/kms_obsidian`
- Branch: `chore/kms-operating-system-20260425`
- HEAD: `f328ffe`
- Dirty: `yes`

### 작동하는 것

- 확인 필요: 주요 build/dependency 파일 요약 없음

### 미완성인 것

- 확인 필요: README/docs와 실제 실행 상태를 기준으로 별도 검증 필요.

### 위험한 것

- 확인 필요: secret, production data, deploy 설정은 이 문서화 단계에서 열람/출력하지 않음.
- OpenClaw mode: `branch_pr` 기준으로만 작업.

### 다음에 닫아야 할 루프

- Repo 운영 대시보드와 LLM Wiki 구조 안정화

## 3. 제품/기술 North Star

- 확인된 repo 문서와 현재 운영 목표를 바탕으로, 작고 검증 가능한 루프를 반복해 완성도를 높인다.

## 4. 이번 주 목표

- [ ] README/docs 기반 현재 상태를 한 번 더 검증한다.
- [ ] 다음 실행 큐 1개를 plan으로 닫는다.

## 5. OpenClaw 작업 큐

> OpenClaw는 이 섹션 또는 별도 `OpenClaw-Queue.md`에 있는 일만 수행한다.

- [ ] #openclaw mode:plan priority:P1 README/docs 기반 현재 상태 요약

## 6. 결정사항

| 날짜 | 결정 | 이유 | 되돌릴 조건 |
|---|---|---|---|
| 2026-04-25 | 개인 개발 운영체제 관리 대상에 등록 | 공유대화/운영 프롬프트 기준 | repo 운영 대상에서 제외될 때 |

## 7. 배운 것 / 인사이트

## 8. 관련 문서

- [[OpenClaw-Queue]]
- [[Weekly-Review]]
- [[Decisions]]

## 9. 확인된 근거

### `README.md`

Headings: # ⚙️ 셋업 가이드 (이 파일 먼저 읽기), ## 🚀 5분 셋업 체크리스트, ### 1. Vault 열기, ### 2. 기본 설정, ### 3. 커뮤니티 플러그인 설치, ### 4. 핵심 노트 즐겨찾기, ### 5. 첫 데일리 노트 만들기, ## 📁 폴더 구조 한눈에

Excerpt: --- type: setup created: 2026-04-20 --- # ⚙️ 셋업 가이드 (이 파일 먼저 읽기) > 이 파일은 **옵시디언 최초 설정용**입니다. 일상 사용은 [[🏠 Home]]에서 시작하세요. ## 🚀 5분 셋업 체크리스트 ### 1. Vault 열기
