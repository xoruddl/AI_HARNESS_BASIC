# 코드 리뷰 (CodeRabbit)

설정: [.coderabbit.yaml](../.coderabbit.yaml)

## 확인

PR 생성 후 사용자가 리뷰 확인을 요청하면 조회한다.

```bash
gh pr view <PR번호> --json reviews,comments
gh api repos/{owner}/{repo}/pulls/<PR번호>/comments
```

- 리뷰가 없으면 "리뷰 없음" 한 줄 보고 후 넘어간다. 대기·재조회하지 않는다.
- Summary, Walkthrough 코멘트는 판단 대상이 아니다.

## 판단 기준

| 판단 | 기준 |
| --- | --- |
| 반영 | 버그, 보안, 예외 누락, 프로젝트 규칙 위반, 명확한 가독성 개선 |
| 보류 | 맞는 말이지만 PR 범위 밖. 별도 이슈로 분리 제안 |
| 거절 | 오탐, 취향 차이, 프로젝트 규칙과 충돌, 불필요한 추상화 |

- Nitpick 은 수정 비용이 작고 규칙에 맞을 때만 반영.
- 판단 근거는 `docs/` 규칙 또는 코드 사실로 댄다.

## 보고 형식

```
| # | 위치 | 지적 | 판단 | 근거 |
| 1 | OrderService.java:42 | null 체크 누락 | 반영 | 외부 입력값 |
| 2 | Order.java:10 | Builder 패턴 제안 | 거절 | 필드 3개, 생성자로 충분 |
```

## 반영

- 사용자 확인 후 진행한다.
- 코멘트 하나 = 커밋 하나. 커밋 루프는 [workflow.md](workflow.md) 와 같다.
- 리뷰 스레드 답글은 사용자 승인 후에만 단다. 짧게 쓴다.
  - `반영했습니다. (abc1234)`
  - `PR 범위 밖이라 #15 로 분리했습니다.`
