## 배경
- 소프트웨어 개발에서 요구사항은 항상 변한다.
- 이러한 요구사항을 반영하면서도 엔지니어링적인 비용이 가장 최소화될 수 있으면 좋다.
- 그뿐 아니라 새로 추가한 기능은 쉽게 구현할 수 있어야 하며 장기적인 관점에서 유지보수가 쉬어야 한다.

## 동작방식
- 아직은 어떻게 실행할 것인지 결정하지 않은 코드 블럭을 의미
- 즉, 코드 블럭의 실행은 나중으로 미뤄진다.
- 결과적으로 코드 블럭에 따라 메서드의 동작이 파라미터화된다.

1. 참 또는 거짓을 반환하는 함수를 프레디케이트라고 한다.
2. 선택 조건을 결정하는 인터페이스를 정의하자.

```java
    public interface ApplePredicate {
        boolean test(Apple apple);
    }
```

```java
  public class AppleHeavyWeightPredicate implements ApplePredicate {
      @Override
      public boolean test(Apple apple) {
          return apple.weight() > 200;
      }
  }
```

```java
  public class AppleGreenColorPredicate implements ApplePredicate {
      @Override
      public boolean test(Apple apple) {
          return GREEN.equals(apple.color());
      }
  }
```
<img width="734" alt="스크린샷 2022-09-15 오후 11 31 23" src="https://user-images.githubusercontent.com/59434443/190432841-5890b4df-0126-498b-9c60-93ff34e8df48.png">





