# Constructor Injection을 사용해야 하는 이유
1. 객체의 불변성 확보
- 수정자 주입이나 일반 메소드 주입을 이용하면 불필요하게 수정의 가능성을 열어두어 유지보수성을 떨어뜨린다. 그러므로 생성자 주입을 통해 변경의 가능성을 배제하고 불변성을 보장하는 것이 좋다.
2. 테스트 코드의 작성
- 테스트 코드에서 @Autowired를 사용하기 위해 스프링을 사용하면 단위 테스트가 아닐 뿐만 아니라, 컴포넌트들을 등록하고 초기화하는 시간 때문에 테스트 비용이 증가하게 된다. 그렇다고 대안으로 리플렉션을 사용하면 깨지기 쉬운 테스트가 된다.   
반면에 생성자 주입을 사용하면 컴파일 시점에 객체를 주입받아 테스트 코드를 작성할 수 있으며, 주입하는 객체가 누락된 경우 컴파일 시점에 오류를 발견할 수 있다. 심지어 우리가 테스트를 위해 만든 Test객체를 생성자로 넣어 편리함을 얻을 수도 있다.
3. final 키워드 작성 및 Lombok과의 결합
- 생성자 주입을 사용하면 필드 객체에 final 키워드를 사용할 수 있으며, 컴파일 시점에 누락된 의존성을 확인할 수 있다. 반면에 다른 주입 방법들은 객체의 생성(생성자 호출) 이후에 호출되므로 final 키워드를 사용할 수 없다.
4. 스프링에 비침투적인 코드 작성
- 필드 주입을 사용하려면 @Autowired를 이용해야 하는데, 이것은 스프링이 제공하는 어노테이션이다. 그러므로 @Autowired를 사용하면 다음과 같이 UserService에 스프링 의존성이 침투하게 된다.
- 스프링이 없이 코드가 작성되면 더욱 유연한 코드를 확보하게 된다. 프레임워크가 자주 바뀌는 것도 아니므로 비록 스프링 코드가 침투하는게 치명적인 문제는 아니긴하다. 하지만 그래도 더 좋은 방법(생성자 주입)이 있는데, 굳이 사용할 필요는 없다.
5. 생성자 주입을 사용하면 애플리케이션 구동 시점(객체의 생성 시점)에 순환 참조 에러를 예방할수 있다

```java
@Service
public class UserService {

    @Autowired
    private MemberService memberService;
    
    @Override
    public void register(String name) {
        memberService.add(name);
    }

}

@Service
public class MemberService {

    @Autowired
    private UserService userService;

    public void add(String name){
        userService.register(name);
    }

}

new UserService(new MemberService(new UserService(new MemberService()...))) //이런식으로 스택오버플로우 발생 -> 서버가죽음
```
