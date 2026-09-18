# 브랜치 전략

GitHub Flow 기반.

## 브랜치

| 브랜치 | 용도 |
| --- | --- |
| `main` | 항상 빌드 가능한 상태. 직접 커밋·push 금지 |
| `<type>/<이슈번호>-<설명>` | 작업 브랜치. main 에서 분기 |

- `type` 은 커밋 타입과 같다. (`feat`, `fix`, `refactor`, `docs`, `test`, `chore` ...)
- 설명은 영어 소문자 + 하이픈, 3~4단어.
- 이슈가 없으면 번호 생략.

```
feat/12-order-cancel
fix/login-redirect-loop
docs/commit-convention
```

## 규칙

- 브랜치 하나 = PR 하나 = 목적 하나.
- 브랜치 수명은 짧게. 커밋 10개를 넘기면 PR 을 나눈다.
- main 최신화는 rebase: `git fetch origin && git rebase origin/main`
- push 된 브랜치를 rebase 했다면 `git push --force-with-lease` 만 쓴다. `--force` 금지.

## 병합

- PR 로만 main 에 병합한다.
- 방식: **Rebase and merge**. 작은 커밋 이력을 그대로 남긴다.
- Squash merge 는 쓰지 않는다.
- 병합 후 작업 브랜치 삭제.
