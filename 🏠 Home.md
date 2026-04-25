---
type: home
created: 2026-04-20
---
# 🏠 Home

> **여기서부터 시작하세요.** 이 노트가 Vault의 메인 입구입니다. 즐겨찾기에 추가해두세요. (별 모양 아이콘 클릭)

## 📌 자주 쓰는 곳

### 오늘의 작업
- [[2026-04-20]] - 오늘의 데일리 노트 (없으면 `Ctrl+P` → "오늘의 일일 노트")

### 진행 중인 프로젝트
- 🏢 회사: [[AI-TF]] · [[연말정산-TF]]
- 🌱 사이드: [[연말정산모듈]]

### 자기개발
- [[학습로그]] · [[독서리스트]]

---

## 🗺 폴더별 입구

| 폴더 | 무엇 | 입구 노트 |
|------|------|-----------|
| 📥 00_Inbox | 분류 미정인 메모 | (그냥 새 노트 던지기) |
| 📁 01_Projects | 끝이 있는 작업 | [[Projects]] |
| 🌱 02_Areas | 꾸준히 하는 영역 | [[Areas]] |
| 📚 03_Resources | 참고자료 | [[Resources]] |
| 🗄 04_Archive | 완료/중단 | [[Archive]] |
| 🤝 05_Meetings | 회의록 | [[Meetings]] |
| 📅 06_Daily | 일일 노트 | [[Daily]] |

---

## 🚀 처음이라면 이 순서로

1. **`README.md` 읽기** - 옵시디언 설정 가이드 (플러그인 설치 등)
2. **이 Home 노트 즐겨찾기** (별표 클릭)
3. **오늘 데일리 노트 만들기** - `Ctrl+P` → "오늘의 일일 노트"
4. **회의 한 번 해보기** - `05_Meetings/2026/04/`에 회의록 만들고 본문에 `[[AI-TF]]` 입력
5. **MOC에서 백링크 확인** - [[AI-TF]] 열어서 우측 백링크 패널 보기

---

## 💡 핵심 사용 원칙

- **링크가 폴더보다 중요** - `[[프로젝트명]]` 으로 어디서든 점프
- **MOC = 입구 노트** - 폴더에 들어가면 동명의 `.md` 파일이 그 폴더의 안내자
- **데일리 노트가 매일의 출발점** - 그날 한 일/회의/생각을 모두 링크로 연결
- **고민되면 일단 `00_Inbox`** - 정리는 나중에

---

## 📊 전체 진행 중 작업 (자동)

```dataview
TABLE status, file.folder as "위치"
FROM "01_Projects"
WHERE type = "project" AND status = "active"
SORT file.mtime DESC
```

> ⚠️ 위 표는 **Dataview 플러그인 설치 후** 자동으로 채워집니다. 설치 전엔 코드 블록으로 보여요.

# Repo Operating Dashboard

## Active Projects

```dataview
TABLE lane, maturity, priority, openclaw_mode, next_action, last_reviewed
FROM "01_Projects"
WHERE type = "project"
SORT priority ASC, last_reviewed ASC
```

## OpenClaw Control

- [[08_Automation/openclaw/Runbook]]
- [[08_Automation/openclaw/Permission-Policy]]
- [[08_Automation/openclaw/Command-Catalog]]
- [[08_Automation/openclaw/Execution-Log]]
- [[08_Automation/openclaw/Repo-Sync-Report]]
- [[08_Automation/openclaw/Prompt-Library]]

## LLM Wiki

- [[07_LLM_Wiki/index]]
- [[07_LLM_Wiki/_system/contradictions]]
- [[07_LLM_Wiki/_system/stale-pages]]

## Product Projects

- [[01_Projects/Products/VibeGrid/VibeGrid]]
- [[01_Projects/Products/VibeHR/VibeHR]]
- [[01_Projects/Products/VibeRec/VibeRec]]
- [[01_Projects/Products/TripCart/TripCart]]

## Work / Tool Projects

- [[01_Projects/Work/Jarvis/Jarvis]]
- [[01_Projects/Work/EHR-Harness-Plugin/EHR-Harness-Plugin]]

## Public Surface

- [[01_Projects/Public/Blog/Blog]]
- [[01_Projects/Public/Landing/Landing]]
