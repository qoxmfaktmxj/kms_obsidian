# OpenClaw Permission Policy

## 기본 원칙

1. Obsidian queue 없는 작업은 실행하지 않는다.
2. main/master branch 직접 push 금지.
3. 회사/업무 데이터는 read_only 또는 plan_only.
4. production secret 접근 금지.
5. 모든 실행은 Execution-Log에 기록.
6. 실패하면 재시도보다 보고를 우선한다.
7. dirty repo는 자동 pull하지 않는다.
8. `git reset --hard`, `git clean -fd`, `rm -rf` 금지.
9. 승인 없는 코드 수정 금지.
10. token, secret, cookie, private key를 출력하지 않는다.

## Repo별 권한

| Repo | Mode | 이유 |
|---|---|---|
| kms_obsidian | branch_pr | control plane 문서화 대상 |
| jarvis | plan_only | 업무성 프로젝트, 회사 맥락 주의 |
| ehr-harness-plugin | plan_only | 배포 중인 도구, 안전성 우선 |
| vibe-grid | branch_pr | 테스트/품질 개선 자동화 적합 |
| vibe-hr | plan_only | HR 도메인 복잡도 큼 |
| vibe-rec | branch_pr | SaaS 데모 완성에 적합 |
| tripcart | branch_pr | 개인 실험 프로젝트 |
| qoxmfaktmxj.github.io | branch_pr | 블로그 자동화 대상 |
| landing-minseok91 | read_only | 현재는 유지보수 표면 |
