# 클린 코드 예시

원칙은 [clean-code.md](clean-code.md).

## 조기 반환

```java
// Bad
public int discount(Member member) {
  if (member != null) {
    if (member.isActive()) {
      return member.isVip() ? 20 : 10;
    }
  }
  return 0;
}

// Good
public int discount(Member member) {
  if (member == null || !member.isActive()) {
    return 0;
  }
  return member.isVip() ? VIP_RATE : DEFAULT_RATE;
}
```

## 매직 넘버

```java
// Bad
if (password.length() < 8) { ... }

// Good
/** 보안 정책 v2 기준 최소 길이. */
private static final int MIN_PASSWORD_LENGTH = 8;

if (password.length() < MIN_PASSWORD_LENGTH) { ... }
```

## boolean 플래그 파라미터

```java
// Bad
sendMail(user, true);

// Good
sendWelcomeMail(user);
sendReminderMail(user);
```

## Tell, Don't Ask

```java
// Bad
if (order.getStatus() == Status.PAID && order.getPaidAt().isAfter(limit)) {
  order.setStatus(Status.CANCELED);
}

// Good
order.cancel(limit);
```

## 원시 값 포장

```java
// Bad
public void register(String email) {
  if (!email.contains("@")) throw new IllegalArgumentException();
  ...
}

// Good
public record Email(String value) {
  public Email {
    if (value == null || !value.contains("@")) {
      throw new InvalidEmailException(value);
    }
  }
}
```

## 예외 처리

```java
// Bad
try {
  payment.approve();
} catch (Exception e) {
}

// Good
try {
  payment.approve();
} catch (PgTimeoutException e) {
  // PG 타임아웃은 승인 여부가 불확실하므로 조회 후 재처리 대상에 넣는다.
  throw new PaymentPendingException(payment.id(), e);
}
```

## SRP

```java
// Bad: 주문 저장, 메일 발송, 포인트 적립이 한 클래스에
class OrderManager {
  void order(...) { save(); sendMail(); addPoint(); }
}

// Good: 책임별로 나누고 조합
class OrderService {
  private final OrderRepository orders;
  private final OrderNotifier notifier;
  private final PointRewarder rewarder;
}
```

## OCP (타입별 분기 제거)

```java
// Bad: 결제 수단 추가마다 switch 수정
int fee(PayType type, int amount) {
  switch (type) {
    case CARD: return amount * 3 / 100;
    case BANK: return 500;
    default: throw new IllegalArgumentException();
  }
}

// Good: 새 수단은 구현체만 추가
interface FeePolicy {
  int fee(int amount);
}

class CardFeePolicy implements FeePolicy {
  public int fee(int amount) { return amount * 3 / 100; }
}
```

## LSP

```java
// Bad: 상위 계약을 깨는 하위 타입
class ReadOnlyList<E> extends ArrayList<E> {
  @Override public boolean add(E e) { throw new UnsupportedOperationException(); }
}

// Good: 필요한 계약만 가진 타입을 쓴다
List<E> items = List.copyOf(source);
```

## ISP

```java
// Bad
interface Worker { void work(); void eat(); }
class Robot implements Worker { public void eat() { } } // 빈 구현

// Good
interface Workable { void work(); }
interface Eatable { void eat(); }
class Robot implements Workable { ... }
```

## DIP

```java
// Bad: 구체 클래스를 직접 생성
class OrderService {
  private final MySqlOrderRepository repository = new MySqlOrderRepository();
}

// Good: 추상에 의존, 생성자 주입
class OrderService {
  private final OrderRepository repository;

  OrderService(OrderRepository repository) {
    this.repository = repository;
  }
}
```
