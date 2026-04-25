# Weekly Review - VibeGrid

## Review Date

- 2026-04-25 UTC

## 이번 주 확인

- [x] README/AGENTS/CHANGELOG와 실제 코드 상태 차이 확인
- [x] Public API export 표면 확인
- [x] E2E/unit test 현황 확인
- [x] clipboard/excel/persistence 취약 영역 우선순위 정리
- [x] VibeHR 이식 전 선결 조건 정리

## 확인한 현재 상태

- VibeGrid는 `README.md`와 `docs/release/public-api-stability.md` 기준으로 내부 파일럿 사용은 가능하다.
- `@vibe-grid/core`와 `@vibe-grid/react`가 주 소비 표면이다.
- Stable API와 Experimental API가 root export에 섞여 있어 소비 앱이 잘못 의존할 위험이 있다.
- TanStack은 props 레벨로 직접 노출되지는 않지만, `@vibe-grid/tanstack-adapter` export가 열려 있어 문서/allowlist로 소비 금지를 명확히 해야 한다.
- E2E는 Grid Lab/Bench/Compatibility/Employee Batch 중심으로 비교적 넓다.
- Unit은 bulk orchestration과 React bulk hook에만 존재한다.
- `npm run test:core`는 node_modules 미설치로 실패했다. 현재 repo checkout에는 `node_modules`와 `node_modules/.bin/tsc`가 없다.

## Decisions

- VibeHR 이식은 전면 교체가 아니라 adapter + pilot route/low-risk screen 방식이 적절하다.
- Excel이 `clipboard/excel/persistence` 중 가장 취약하다.
- Persistence는 e2e reload 검증은 있으나 scope/key/invalid JSON unit 보강이 필요하다.
- Clipboard는 e2e 커버가 상대적으로 좋지만 순수 함수 unit 보강이 필요하다.

## Updated Docs

- `Public-API.md`
- `QA-Matrix.md`
- `VibeHR-Integration.md`
- `OpenClaw-Queue.md`

## Next Actions

- [ ] Excel roundtrip/header mismatch/template schema unit test 추가
- [ ] Persistence storage key/scope/isolation/invalid JSON unit test 추가
- [ ] Clipboard parse/overflow/readonly/validation unit test 추가
- [ ] VibeHR adapter 설계 문서 작성 후 R2 승인 단위로 pilot screen 선정
