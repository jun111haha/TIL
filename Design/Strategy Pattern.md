# 전략패턴
전략 패턴은 한 유형의 알고리즘을 보유한 상태에서 런타임에 적절한 알고리즘을 선택하는 기법.   
다양한 기준을 갖는 입력값을 검증하거나, 다양한 파싱 방법을 사용하거나, 입력 형식을 설정하는 등 다양한 시나리오에 전략 패턴을 활용 할 수 있다.

1. String 문자열을 검증하는 인터페이스 생성
```java
public interface ValidationStrategy {
  boolean execute(String s)
}
```
2. 위에서 정의한 인터페이스를 구현하는 클래스를 정의
```java
public class IsAllLowerCase implements ValidationStrategy {
  public boolean execute(String s){
    return s.matches("[a-z]");
  }
}

public class IsNumeric implements ValidationStrategy {
  public boolean execute(String s){
    return s.matches("\\d+");
  }
}

```
3. 구현한 클래스를 다양한 검증 전략으로 활용 가능
```java
public Validator{
  private final ValidationStrategy strategy;
  public Validator(ValidationStrategy v){
    this.strategy = v;
  }
  public boolean validate(String s){
    return  strategy.excute(s);
  }
}

Validator numericValidator = new Validator(new IsNumeric());
boolean b1 = numericValidator.validate("aaa"); //false

Validator lowerCaseValidator = new Validator(new IsAllLowerCase());
boolean b1 = lowerCaseValidator.validate("bbbb"); //true
```

- 람다 표현식으로 사용
ValidationStrategy 는 함수형 인터페이스며 Predicate<String> 과 같은 함수 디스크립터를 갖고 있음을 파악 했다.
따라서 다양한 전략을 구현하는 새로운 클래스를 구현할 필요 없이 람다 표현식을 직접 전달하면 코드가 간결해진다.
