# Jarvis LLM Wiki Architecture

## Operating Model

- raw source는 입력 재료다.
- compiled wiki page가 장기 지식의 정본이다.
- query는 raw chunk보다 compiled wiki를 우선 읽는다.
- lint/report는 stale page, contradiction, missing source를 드러낸다.

## 확인 필요

- Jarvis repo의 ingest/query/lint 실제 구현 범위
- wiki page 최소 schema
- disk/git과 DB projection의 책임 경계
