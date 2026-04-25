---
type: project
status: active
lane: product
repo: https://github.com/qoxmfaktmxj/vibe-rec
local_path: ~/dev/qoxmfaktmxj/vibe-rec
maturity: prototype
priority: P1
openclaw_mode: branch_pr
cadence: weekly
last_reviewed: 2026-04-25
next_action: "지원자 플로우와 관리자 검토 플로우를 닫힌 SaaS 데모로 완성"
tags: [project, saas, recruiting, backend, demo]
---

# VibeRec

## 1. 한 문장 정의

채용/추천 계열 SaaS 후보.

## 2. 현재 상태

- Local path: `~/dev/qoxmfaktmxj/vibe-rec`
- Branch: `main`
- HEAD: `60073c3`
- Dirty: `no`

### 작동하는 것

- 확인 필요: 주요 build/dependency 파일 요약 없음

### 미완성인 것

- 확인 필요: README/docs와 실제 실행 상태를 기준으로 별도 검증 필요.

### 위험한 것

- 확인 필요: secret, production data, deploy 설정은 이 문서화 단계에서 열람/출력하지 않음.
- OpenClaw mode: `branch_pr` 기준으로만 작업.

### 다음에 닫아야 할 루프

- 지원자 플로우와 관리자 검토 플로우를 닫힌 SaaS 데모로 완성

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

Headings: # vibe-rec, ## 주요 화면, ### 채용 공고 보드, ### 공고 상세와 지원 상태, ### 프로필 선작성, ### 관리자 지원자 운영, ## 스택, ## 로컬 실행

Excerpt: # vibe-rec vibe-rec는 공고 탐색, 프로필 작성, 지원서 제출, 관리자 검토를 한 흐름으로 연결한 채용 운영 제품입니다. ## 주요 화면 ### 채용 공고 보드 ![채용 공고 보드](docs/readme/jobs-board-current.png) 지원 가능한 공고를 기본값으로 보여주고, 신입/경력/상시 채용과 키워드 검색으로 바로 좁힐 수 있습니다. ### 공고 상세와 지원 상태 ![공고 상세](docs/readme/job-detail-current.png)

### `AGENTS.md`

Headings: # vibe-rec (HireFlow), ## Purpose, ## Key Files, ## Subdirectories, ## For AI Agents, ### Operating Rules, ### Architecture Overview, ### Stack

Excerpt: # vibe-rec (HireFlow) ## Purpose Recruitment operations product that connects job posting discovery, profile creation, application submission, and admin review into a single flow. The product name is **HireFlow**; the repo name is `vibe-rec`. ## Key Files | File | Description | |------|-------------| | `compose.deploy.yaml` | Docker Compose for postgres, api, and web services | | `DESIGN.md` | Design system master document (colors, typography, spacing, components) |

### `CLAUDE.md`

Headings: # vibe-rec (HireFlow), ## 빌드 & 테스트, # API, # Web, # DB, ## 핵심 규칙, ### 1. 디자인 시스템 (DESIGN.md), ### 2. Flyway 마이그레이션 (append-only)

Excerpt: # vibe-rec (HireFlow) 모노레포 채용 운영 플랫폼. Next.js 16 프론트엔드(`apps/web`) + Spring Boot 4 API(`apps/api`) + PostgreSQL 16. ## 빌드 & 테스트 ```bash # API cd apps/api && ./gradlew.bat bootRun --args=--server.port=8080   # 실행 cd apps/api && ./gradlew.bat classes --console=plain              # 컴파일 cd apps/api && ./gradlew.bat test --console=plain                 # 테스트 (Testcontainers)

### 문서/워크플로 후보

- `docs/AGENTS.md`
- `docs/architecture.md`
- `docs/auth-flows.md`
- `docs/demo/EXECUTIVE_DEMO_90S_TYPED.md`
- `docs/local-development.md`
- `docs/readme/admin-current.png`
- `docs/readme/job-detail-current.png`
- `docs/readme/jobs-board-current.png`
- `docs/readme/profile-current.png`
- `docs/screenshots/03-job-detail.png`
- `docs/screenshots/04-login.png`
- `docs/screenshots/05-admin-login.png`
- `docs/testing.md`
- `.github/workflows/ci.yml`
