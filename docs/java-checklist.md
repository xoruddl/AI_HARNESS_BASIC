# 자바 클린 코드 체크리스트

Java 코드 작성·리뷰 시 확인한다. [clean-code.md](clean-code.md) 와 겹치면 이 문서가 우선한다.

| # | 체크 항목 |
| --- | --- |
| 1 | 자바 코드 컨벤션을 지켰는가 |
| 2 | 메서드 들여쓰기가 1단계인가 |
| 3 | `else` 를 쓰지 않았는가 |
| 4 | 원시값과 문자열을 포장했는가 |
| 5 | 컬렉션에 일급 컬렉션을 적용했는가 |
| 6 | 인스턴스 변수가 2개 이하인가 |
| 7 | 도메인 객체에 getter/setter 가 없는가 |
| 8 | 메서드 인자가 3개 이하인가 |
| 9 | 한 줄에 점(`.`)이 하나인가 |
| 10 | 메서드가 한 가지 일만 하는가 |
| 11 | 클래스가 작은가 |

## 1. 자바 코드 컨벤션

- [Google Java Style Guide](https://google.github.io/styleguide/javaguide.html) 를 따른다.
- IntelliJ 또는 Eclipse 에서 포맷팅한다.
- IDE 포맷터는 google-java-format 기준으로 맞춘다. 최종 판정은 `spotlessCheck`. → [lint-and-ci.md](lint-and-ci.md)

## 2. 들여쓰기 1단계

- 메서드 안의 들여쓰기는 1단계만 허용한다.
- 중첩이 생기면 안쪽 블록을 메서드로 추출한다.

## 3. else 금지

- `else` 를 쓰지 않는다. 조기 반환으로 바꾼다.

```java
// 나쁨
if (score >= 60) {
    return PASS;
} else {
    return FAIL;
}

// 좋음
if (score >= 60) {
    return PASS;
}
return FAIL;
```

## 4. 원시값·문자열 포장

- 의미 있는 원시값과 문자열은 클래스로 포장한다.
- 검증 로직은 포장 클래스 생성자에 둔다.

```java
public class Money {
    private final int amount;

    public Money(int amount) {
        // 음수 금액은 도메인상 존재할 수 없으므로 생성 시점에 막는다.
        if (amount < 0) {
            throw new IllegalArgumentException("금액은 0 이상이어야 한다.");
        }
        this.amount = amount;
    }
}
```

## 5. 일급 컬렉션

- 컬렉션은 그 컬렉션만 필드로 가진 클래스로 감싼다.
- 컬렉션 관련 로직(검증, 합계, 필터)은 일급 컬렉션 안에 둔다.

```java
public class Lottos {
    private final List<Lotto> lottos;

    public Lottos(List<Lotto> lottos) {
        this.lottos = List.copyOf(lottos);
    }

    public int countWinning(WinningNumbers winning) { ... }
}
```

## 6. 인스턴스 변수 2개 이하

- 3개 이상의 인스턴스 변수를 가진 클래스를 만들지 않는다.
- 어렵다면 최소한 줄이려고 시도한다. 관련 있는 필드끼리 객체로 묶는다.

## 7. getter/setter 금지

- 핵심 로직을 담은 도메인 객체에는 getter/setter 를 쓰지 않는다.
- 값을 꺼내 판단하지 않고 객체에 메시지를 보낸다.
- DTO 는 허용한다.

## 8. 메서드 인자 3개 이하

- 4개 이상의 인자는 허용하지 않는다.
- 3개도 줄일 수 있는지 먼저 검토한다.

## 9. 한 줄에 점 하나

- 디미터 법칙("친구하고만 대화하라")을 지킨다.
- `location.current.representation.substring(0, 1)` 처럼 점이 여러 개면 리팩터링 대상을 찾는다.

## 10. 메서드는 한 가지 일만

- 메서드 이름으로 하는 일이 다 설명되지 않으면 나눈다.

## 11. 작은 클래스

- 클래스를 작게 유지한다.
- 클래스가 커지면 책임을 나눌 수 있는지 먼저 본다.
