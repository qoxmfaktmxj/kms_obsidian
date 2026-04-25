---
type: project
status: active
lane: public
repo: https://github.com/qoxmfaktmxj/landing-minseok91
local_path: ~/dev/qoxmfaktmxj/landing-minseok91
maturity: usable
priority: P3
openclaw_mode: read_only
cadence: paused
last_reviewed: 2026-04-25
next_action: "현재는 블로그/랜딩 표면으로 유지"
tags: [project, landing, public]
---

# Landing

## 1. 한 문장 정의

랜딩 페이지 / 공개 포트폴리오 표면.

## 2. 현재 상태

- Local path: `~/dev/qoxmfaktmxj/landing-minseok91`
- Branch: `main`
- HEAD: `138f8d1`
- Dirty: `no`

### 작동하는 것

- package name: `relaxed-diffie`
- npm scripts: build, dev, lint, start
- dependencies: `clsx`, `framer-motion`, `lucide-react`, `next`, `react`, `react-dom`, `tailwind-merge`
- devDependencies: `@eslint/eslintrc`, `@types/node`, `@types/react`, `@types/react-dom`, `eslint`, `eslint-config-next`, `postcss`, `tailwindcss`, `typescript`

### 미완성인 것

- 확인 필요: README/docs와 실제 실행 상태를 기준으로 별도 검증 필요.

### 위험한 것

- 확인 필요: secret, production data, deploy 설정은 이 문서화 단계에서 열람/출력하지 않음.
- OpenClaw mode: `read_only` 기준으로만 작업.

### 다음에 닫아야 할 루프

- 현재는 블로그/랜딩 표면으로 유지

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

Headings: # Minseok Landing Page, ## 기술 스택, ## 로컬 실행, ## 스크립트, ## 프로젝트 구조, ## 목적

Excerpt: # Minseok Landing Page 민석을 소개하고 주요 프로젝트와 연락처를 정리한 개인 랜딩 페이지입니다. 프로필, 기술 스택, 프로젝트 소개, 연락 채널을 한 페이지에 담은 포트폴리오 성격의 웹사이트입니다. ## 기술 스택 - Next.js 16 - React 19 - TypeScript - Tailwind CSS
