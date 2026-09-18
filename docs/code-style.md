# 코드 스타일

## 포맷

- google-java-format (Spotless). 수동 정렬하지 않는다.
- 커밋 전 `./gradlew spotlessApply`. pre-commit 훅이 `spotlessCheck` 를 돌린다.
- 설정은 [lint-and-ci.md](lint-and-ci.md).

## 네이밍

| 대상 | 규칙 | 예 |
| --- | --- | --- |
| 클래스 | 명사, PascalCase | `OrderCanceler` |
| 메서드 | 동사, camelCase | `cancelOrder()` |
| boolean | `is/has/can` 접두 | `isCancelable()` |
| 상수 | UPPER_SNAKE_CASE | `MAX_RETRY_COUNT` |
| 컬렉션 | 복수형 | `orders` |

- 축약어 금지. (`ord`, `mgr`, `tmp`)
- 타입을 이름에 넣지 않는다. (`orderList` → `orders`)

## 주석

주석은 적극적으로 단다. 단, 코드를 반복하지 말고 **의도와 이유**를 쓴다.

필수:

- public 클래스·메서드: Javadoc. 역할, 파라미터 제약, 반환값, 예외.
- 비즈니스 규칙·정책 값: 출처나 이유.
- 비자명한 로직: 왜 이렇게 했는지.
- 우회 코드: 원인과 제거 조건.

형식:

- TODO: `// TODO(작성자): 내용 #이슈번호`
- 한 줄 주석은 대상 코드 바로 위에.

금지:

- 코드를 그대로 읽는 주석 (`// i 증가`)
- 주석 처리된 코드
- 변경 이력 주석 (git 이 한다)

```java
/**
 * 주문을 취소한다.
 *
 * @param orderId 취소할 주문 ID. null 불가
 * @throws OrderNotCancelableException 결제 후 24시간이 지난 경우
 */
public void cancel(Long orderId) {
  Order order = orderRepository.getById(orderId);

  // 정산이 결제 후 24시간 시점에 확정되므로 그 이후 취소는 환불 절차로 처리한다.
  if (order.isPaidBefore(CANCEL_LIMIT)) {
    throw new OrderNotCancelableException(orderId);
  }
  order.cancel();
}
```

설계 원칙은 [clean-code.md](clean-code.md), 예시는 [clean-code-examples.md](clean-code-examples.md).
