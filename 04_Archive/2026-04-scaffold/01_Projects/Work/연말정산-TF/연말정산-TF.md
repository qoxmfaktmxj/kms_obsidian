---
status: active
type: project
tags: [project, work, tf/yearend]
created: 2026-04-20
---
# 연말정산-TF

> 회사 연말정산 Task Force. Javis 디자인 + 패치 관리 페이지 두 갈래로 진행.

## 🎯 목표
- 

## 📌 현재 상태
- 

## 🔗 하위 프로젝트
- [[Javis-디자인]]
- [[패치관리페이지]]

## 🔄 사이드와 연결
- [[연말정산모듈]] - 개인 사이드 프로젝트로, 회사 작업 인사이트 활용 가능

## 📊 진행 중
```dataview
TABLE status, file.mtime as "수정"
FROM "01_Projects/Work/연말정산-TF"
WHERE type = "project" AND file.path != this.file.path
SORT file.mtime DESC
```

## 📅 최근 회의
```dataview
LIST date
FROM "05_Meetings"
WHERE contains(file.outlinks, [[연말정산-TF]]) OR contains(tags, "tf/yearend")
SORT date DESC
LIMIT 10
```

## 🎯 미완료 액션 아이템
```dataview
TASK
FROM "05_Meetings" OR "01_Projects/Work/연말정산-TF"
WHERE !completed
GROUP BY file.link
```

## 📝 메모
- 
