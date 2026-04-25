# OpenClaw Permission Policy

## 기본 원칙

1. Obsidian queue 없는 작업은 실행하지 않는다.
2. 기본은 main/master 직접 수정·push 금지. 단, **석이가 명시적으로 main/master 작업 또는 push/merge를 승인한 경우에만** OpenClaw가 main/master 작업을 수행할 수 있다.
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

## Main/Master 명시 승인 정책

기본값은 안전한 branch 작업이다. 다만 석이가 채팅 또는 queue에서 명시적으로 승인하면 OpenClaw는 main/master 작업도 수행할 수 있다.

명시 승인 예시:
- "main에 바로 반영해"
- "master에서 작업해도 돼"
- "이 변경은 네가 merge/push까지 해"
- queue task에 `approved: true`와 `allow_main: true` 또는 `allow_direct_push: true`가 함께 있는 경우

필수 보고 의무:
1. main/master에 아직 반영되지 않은 branch, commit, local change, unpushed change가 있으면 반드시 석이에게 알린다.
2. 보고에는 repo명, branch명, commit, push/merge 필요 여부, 실행할 명령을 포함한다.
3. OpenClaw가 작업을 끝냈다고 말하기 전에 `git status`, upstream ahead/behind, push 여부를 확인한다.
4. main/master 직접 작업이 허용되더라도 secret 출력, destructive command, production data write는 여전히 금지한다.
