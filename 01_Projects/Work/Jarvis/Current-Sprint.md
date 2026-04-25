# Jarvis Current Sprint

## 이번 주 목표

LLM Wiki ingest/query/lint 중 하나의 닫힌 루프를 완성한다.

## Done Definition

- [ ] raw source 1개 ingest
- [ ] 관련 wiki page N개 생성/수정
- [ ] index/log 갱신
- [ ] query가 raw chunk가 아니라 compiled wiki page를 읽음
- [ ] lint/report 최소 1개 생성

## 금지

- RAG 포털로 회귀 금지
- DB를 wiki body의 진실원천으로 만들지 않기
- raw chunk answer를 최종 답변처럼 쓰지 않기

## Open Questions

- [ ] 어떤 raw source부터 ingest할 것인가?
- [ ] compiled wiki page의 최소 schema는 무엇인가?
- [ ] lint report의 첫 번째 규칙은 무엇인가?
