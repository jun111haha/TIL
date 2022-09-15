# 배경
- 소프트웨어 개발에서 요구사항은 항상 변한다.
- 이러한 요구사항을 반영하면서도 엔지니어링적인 비용이 가장 최소화될 수 있으면 좋다.
- 그뿐 아니라 새로 추가한 기능은 쉽게 구현할 수 있어야 하며 장기적인 관점에서 유지보수가 쉬어야 한다.

# 동작방식
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
```java
  public List<Apple> filterApples(List<Apple> inventory, ApplePredicate applePredicate) {
      final var result = new ArrayList<Apple>();
      for (final var apple : inventory) {
          if (applePredicate.test(apple)) {
              result.add(apple);
          }
      }
      return result;
  }
```
3. 필요한 조건에 따라 ApplePredicate를 만들어서 filterApples 메서드에 전달해 주기만 하면 된다.
4. 이렇게 우리가 전달한 ApplePredicate 객체에 의해 filterApples 메서드의 동작이 결정된다.

```java
 public class AppleRedAndHeavyPredicate implements ApplePredicate {
        @Override
        public boolean test(Apple apple) {
            return RED.equals(apple.color()) &&
                    apple.weight() > 180;
        }
    }
```

<img width="741" alt="스크린샷 2022-09-15 오후 11 31 16" src="https://user-images.githubusercontent.com/59434443/190434094-6a3090e3-3a7b-4888-a967-a4bb6ef5563e.png">

위의 그림에서 보여주는 것처럼 ApplePredicate의 실제 구현은 test 메서드에 있다.

안타깝게도 메서드는 객체만 인수로 받으므로 test 메서드를 ApplePredicate 객체로 감싸서 전달해야 한다.

Java 8에 새롭게 추가된 람다 표현식을 이용하게 되면 여러 개의 ApplePredicate를 정의하지 않고도 test 메서드의 내부 구현 filter 메서드로 전달할 수 있다.

<img width="734" alt="스크린샷 2022-09-15 오후 11 31 23" src="https://user-images.githubusercontent.com/59434443/190432841-5890b4df-0126-498b-9c60-93ff34e8df48.png">

위 조건에 따라 filter 메서드가 다르게 동작할 것이라고 예상할 수 있다.

이를 전략 디자인 패턴(strategy design pattern)이라고 부른다.

> 전략 디자인 패턴은 각 알고리즘(전략이라 불리는)을 캡슐화하는 알고리즘 패밀리를 정의해둔 다음에 런타임에 알고리즘을 선택하는 기법이다.
filterApples에서 ApplePredicate 객체를 받아 애플의 조건을 검사하도록 메서드를 고쳐야 한다.


이렇게 동작 파라미터화, 즉 메서드가 다양한 동작(또는 전략)을 받아서 내부적으로 다양한 동작을 수행할 수 있다.   

이렇게 하면 filterApples 메서드 내부에서 컬렉션을 반복하는 로직과 컬렉션의 각 요소에 적용할 동작(우리 예제에서는 프레디케이트)을 분리할 수 있다는 점에서 소프트웨어 엔지니어링적으로 큰 이득을 얻는다.

## 출처
모던 자바 인액션

