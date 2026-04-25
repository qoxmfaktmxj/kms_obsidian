---
type: project
status: active
lane: tool
repo: https://github.com/qoxmfaktmxj/ehr-harness-plugin
local_path: ~/dev/qoxmfaktmxj/ehr-harness-plugin
maturity: alpha
priority: P0
openclaw_mode: plan_only
cadence: weekly
last_reviewed: 2026-04-25
next_action: "배포 중 피드백과 수정사항을 Release Log로 분리"
tags: [project, ehr, harness, plugin, ai-agent]
---

# EHR-Harness-Plugin

## 1. 한 문장 정의

EHR 개발 하네스 / 배포형 도구.

## 2. 현재 상태

- Local path: `~/dev/qoxmfaktmxj/ehr-harness-plugin`
- Branch: `main`
- HEAD: `efe7fe6`
- Dirty: `no`

### 작동하는 것

- 확인 필요: 주요 build/dependency 파일 요약 없음

### 미완성인 것

- 확인 필요: README/docs와 실제 실행 상태를 기준으로 별도 검증 필요.

### 위험한 것

- 확인 필요: secret, production data, deploy 설정은 이 문서화 단계에서 열람/출력하지 않음.
- OpenClaw mode: `plan_only` 기준으로만 작업.

### 다음에 닫아야 할 루프

- 배포 중 피드백과 수정사항을 Release Log로 분리

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

Headings: # EHR Harness Plugin, ## 목차, ## 1. 하네스란?, ### 하네스 구조 예시 (EHR5 프로젝트)

Excerpt: # EHR Harness Plugin Oracle 프로시저 기반 레거시 인사시스템(EHR)을 위한 AI 코딩 하네스 자동 생성 플러그인. "하네스 만들어줘" 한 마디로 EHR 프로젝트를 심층 분석하고, 프로젝트에 맞춤화된 하네스를 자동 생성한다. --- ## 목차 1. [하네스란?](#1-하네스란) 2. [플러그인 설치 방법](#2-플러그인-설치-방법) 3. [플러그인 업데이트 방법](#3-플러그인-업데이트-방법)
