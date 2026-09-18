# 작업 흐름

## 1. 시작

- 요구사항이 불명확하면 먼저 질문한다.
- 브랜치를 만든다. → [branch-strategy.md](branch-strategy.md)
- 커밋 계획을 목록으로 제시하고 승인을 받는다.

```
1. Order.java        — feat(order): 주문 취소 사유 필드 추가
2. OrderService.java — feat(order): 주문 취소 로직 추가
3. OrderServiceTest.java — test(order): 주문 취소 테스트 추가
```

## 2. 커밋 루프

1. 파일 하나를 수정한다.
2. 검증한다. (포맷, 빌드, 테스트 — 프로젝트에 있는 것만)
3. 커밋한다. → [commit-convention.md](commit-convention.md)
4. 보고하고 **멈춘다.**

보고 형식:

```
커밋: feat(order): 주문 취소 사유 필드 추가
파일: src/main/java/.../Order.java
다음: OrderService 에 취소 로직 추가 (2/3)
```

- 사용자가 진행 또는 피드백을 주기 전까지 다음 커밋을 하지 않는다.
- 피드백 반영은 새 커밋으로 한다.
- `--amend` 는 사용자가 요청하고, push 전일 때만 쓴다.

## 3. 커밋 크기

- 기본: 파일 1개.
- 묶음 허용: 따로 커밋하면 컴파일·테스트가 깨지는 경우. 최대 3개.
  - 예: 인터페이스 메서드 추가 + 구현체 수정
- 묶을 때: `HARNESS_MAX_FILES=<n> git commit ...` 로 실행하고, 보고에 이유를 한 줄 적는다.
- 테스트는 대상 코드 커밋 바로 다음 커밋으로 분리한다.

## 4. PR

- 계획한 커밋이 끝나면 push 후 PR 을 만든다. → [pull-request.md](pull-request.md)
- PR 링크를 보고하고 멈춘다.
- 리뷰 확인은 [code-review.md](code-review.md).

## 금지

- 멈추지 않고 커밋 여러 개 연속 실행
- 요청 없는 리팩터링·정리 작업 끼워 넣기
- `--no-verify` 등 훅 우회
- main 직접 커밋·push
