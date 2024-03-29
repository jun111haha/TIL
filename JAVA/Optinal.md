# null 때문에 발생하는 문제?
1. 에러의근원 : NullPointerException 은 자바에서 가장 흔히 발생하는 에러
2. 코드를 어지럽힌다 : 때로는 중첩된 null 확인코드를 추가해야 하므로 null 때문에 코드 가독성이 떨어진다.
3. 아무 의미가 없다 : null 은 아무 의미도 표현하지 않는다. 특히 정적 형식 언어에서 값이 없음을 표현하는 방법으로는 적절하지 않다
4. 자바 철학에 위배된다 : 자바는 개발자로부터 모든 포인터를 숨겼다. 하지만 예외가 있는게 null 포인터다
5. 형식 시스템에 구멍을 만든다 : null 은 무형식이며 정보를 포함하고 있지 않으므로 모듬 참조 형식에 null을 할당할 수 있다. 이런식으로 null이 
할당되기 시작하면서 시스템의 다른 부분으로 null 이 퍼졌을 때 애초에 null 이 어떤 의미로 사용되었는지 알 수 없음.

## 자바8 java.util.Optinal<T> 클래스 등장
Optinal은 선택형값을 캡슐화하는 클래스이다. 예를 들어 어떤 사람이 차를 소유하고있지 않다면 Person 클래스의 car 변수는
null 을 가져야 할 것이다. 하지만 새로운 Optinal을 이용할 수 있으므로 null을 할당하는 것이 아니라 변수형을 Optinal<Car>로 설정
값이 없으면 Optinal.empty 메서드로 Optinal 을 반환한다. 특별한 싱글턴 인스턴스를 반화하는 정적 팩토리 메서드임.

 ```java
 public class Peron {
   private Optinal<Car> car; //사람이 차를 소유했을 수도 소유하지 않았을 수도 있으므로 Optinal 로 정의
   public Optinal<Car> getCar(){
     return car;
   }
 }
  
 public class Car {
  private Optinal<Insurance> Insurance; //자동차가 보험을 가입했을수도 안했을수도 있으므로 Optinal 로 정의
  public Optinal<Insurance> getInsurance(){
    return insurance;
    }
  }
  
  public class Insurance {
   private String name; //보험회사는 반드시 존재
   public String getName(){
     return name;
     }
  }
 ```
 
 - Optinal 이 비어있으면 get을 호출했을 때 예외가 발생한다. 
 
 출저 : 자바 인 액션
