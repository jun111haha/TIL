# Singleton Container
1. 싱글톤 컨테이너란 클래스의 인스턴스가 Java JVM 내의 단 하나만 존재
2. 웹 애플리케이션은 수많은 클라이언트에서 서비스를 요청받게 되는데 만약 서버에서 클라이언트의 요청을 받을때마다 클래스 인스턴스를 생성하게 되면 JVM 메모리의 사용량이 증가하게 되고 서버는 부하를 감당 X

- Java 싱글톤 패턴 구현시 문제점
1. 싱글톤 패턴을 구현 코드가 많이 들어간다.
2. 의존관계상 클라이언트가 구체 클래스에 의존 → DIP를 위반한다.
3. 클라이언트가 구체 클래스에 의존 → OCP 원칙 또한 위반할 가능성이 높다.
4. 테스트마다 데이터를 초기화를 해주어야 하므로 까다롭다.
5. 내부 속성을 변경하거나 초기화 하기 어렵다.
6. private 생성자로 자식 클래스를 만들기 어렵다.
7. 결론적으로 유연성이 떨어진다.
8. Anti-패턴으로 불리기도 한다.

- Spring 싱글톤 컨테이너
1. 스프링 컨테이너는 싱글턴 패턴을 적용하지 않아도, 객체 인스턴스를 싱글톤으로 관리한다.
2. 싱글톤 객체를 생성하고 관리하는 기능을 싱글톤 레지스트리라 한다.
3. 스프링 컨테이너에 단일 인스턴스만을 가지는 기능 덕분에 기존의 문제점을 해결하면서 싱글톤으로 유지한다.
4. 싱글톤 패턴을 위한 지저분한 코드가 들어가지 않아도 된다.
5. DIP, OCP, 테스트, private 생성자로 부터 자유롭게 싱글톤을 사용할 수 있다

- 싱글톤 방식의 주의점
객체 인스턴스를 하나만 생성해서 공유하는 싱글톤 방식은 
여러 클라이언트가 하나의 같은 객체 인스턴스를 공유하기 때문에 상태를 유지(stateful)하게 설계하면 안된다.

1. 무상태(stateless)로 설계
2. 특정 클라이언트에 의존적인 필드가 있으면 안된다
3. 특정 클라이언트가 값을 변경할 수 있는 필드가 있으면 X
4. 공유 필드 대신에 자바에서 지역변수, 파라미터, ThreadLocal 등을 사용
5. 스프링 빈의 필드에 공유 값을 설정하면 정말 큰 장애가 발생

## @Configuration
- @Configuration이 있는 경우, 모든 @Bean은 한번씩 호출되지만,
- @Configuration이 없는 경우, 호출될때마다 call 로그가 찍혀 여러번의 호출이 일어나고 싱글톤보장이 안되었다.
 