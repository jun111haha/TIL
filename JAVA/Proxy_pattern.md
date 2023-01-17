# 프록시패턴
- 프록시와 리얼 서브젝트가 공유하는 인터페이스가 있고, 클라이언트는 해당 인터페이스 타입으로 프록시를 사용한다.
- 클라이언트는 프록시를 거쳐서 리얼 서브젝트를 사용하기 때문에 프록시는 리얼 서브젝트에 대한 접근을 관리거나 부가기능을 제공하거나, 리턴값을 변경할 수도 있다.
- 리얼 서브젠트는 자신이 해야 할 일만 하면서(SRP) 프록시를 사용해서 부가적인 기능(접근 제한, 로깅, 트랜잭션, 등)을 제공할 때 이런 패턴을 주로 사용한다.

```java
public interface Subject {
    String request();
}
```

```java
public class RealSubject implements Subject {

    @Override
    public String request() {
        return "HelloWorld";
    }
}

```

```java
public class Proxy implements Subject {

    private final RealSubject realSubject = new RealSubject();

    @Override
    public String request() {
        return realSubject.request();  //프록시가 실제의 메소드를 호출한다.
    }

}
```

```java
public class Main {

    public static void main(String[] args) {
        // Subject클래스의 메소드를 호출하는것이아닌 프록시클래스의 메소드를 호출한다.
        Subject subject = new Proxy();
        System.out.println(subject.request()); // 내부적으로 Subject의 메소드를 호출한다.

    }
}
```

## 프록시패턴 사용하는 이유?
1. 흐름을 제어할수 있다
- 흐름을 제어하가 위한것이 프록시패턴을 이용하는 가장 큰 이유인데 
간단히 말하면 동기적인 처리를 최대한 비동기적으로 처리하기 위함이라고 생각한다.
프록시 객체를 사용하지 않으면, 많은 양의 리소스를 필요로하는 상황에서 디비쿼리가 엄청나게 느려질 수 있다. 
이럴때 지연초기화를 위한 코드작성을 해야하는데 이를 모든 클래스마다 직접 넣어버리면 엄청나게 많은 코드중복이 발생할것이다. (스프링의 AOP 와 흡사)

2. 실제 메소드가 호출되기 이전에 필요한 기능(전처리등의)을 구현객체 변경없이 추가할 수 있다.

3. 캐시를 사용할 수 있다.
- 프록시가 내부캐시를 통해 데이터가 캐시에 존재하지 않는 경우에만 주체클래스에서 작업이 실행되도록 할 수 있다. 

출처 : https://refactoring.guru/design-patterns/proxy
출처 : 백기선 더자바를 조작하는 방법

