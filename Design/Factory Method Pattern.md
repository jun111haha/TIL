# 팩토리 메서드 패턴
1. 팩토리 메서드 패턴(Factory method pattern)은 객체지향 디자인 패턴이다. Factory method는 부모(상위) 클래스에 알려지지 않은 구체 클래스를 생성하는 패턴이며. 자식(하위) 클래스가 어떤 객체를 생성할지를 결정하도록 하는 패턴이기도 하다. 부모(상위) 클래스 코드에 구체 클래스 이름을 감추기 위한 방법으로도 사용한다.

2. 팩토리 패턴은 객체를 사용하는 코드에서 객체 생성 부분을 떼어내 추상화한 패턴이자 상속 관계에 있는 두 클래스에서 상위클래스가 중요한 뼈대를 결정하고, 하위 클래스에서 
객체 생성에 관한 구체적은 내용을 결정하는 패턴이다. 상위 클래스와 하위 클래스가 분리되기 때문에 느슨한 결합을 가지며 상위 클래스에서는 인스턴스 생성 방식에 대해 전혀 알 필요가 없기 때문에
더 많은 유연성을 갖게 된다. 그리고 객체 생성 로직이 떼어져 있기 때문에 코드를 리팩터링하더라도 한 곳만 고치면 되기 떄문에 유지 보수성이 증가.

![factorymethodpattern](https://github.com/jun111haha/TIL/blob/main/img/factory_method_pattern.png)

**정적 팩토리 메서드란? 객체 생성의 역할을 하는 클래스 메서드**

## 생성자와는 어떤 차이가 있나?
1. 이름을 가질 수 있다.
객체는 생성 목적과 과정에 따라 생성자를 구별해서 사용할 필요가 있다. new라는 키워드를 통해 객체를 생성하는 생성자는 내부 구조를 잘 알고 있어야 목적에 맞게 객체를 생성할 수 있다.    하지만 정적 팩토리 메서드를 사용하면 메서드 이름에 객체의 생성 목적을 담아 낼 수 있다.

```java
public class LottoFactory() {
  private static final int LOTTO_SIZE = 6;

  private static List<LottoNumber> allLottoNumbers = ...; // 1~45까지의 로또 넘버

  public static Lotto createAutoLotto() {
    Collections.shuffle(allLottoNumbers);
    return new Lotto(allLottoNumbers.stream()
            .limit(LOTTO_SIZE)
            .collect(Collectors.toList()));
  }

  public static Lotto createManualLotto(List<LottoNumber> lottoNumbers) {
    return new Lotto(lottoNumbers);
  }
  ...
}
```
createAutoLotto와 createMenualLotto 모두 로또 객체를 생성하고 반환하는 정적 팩토리 메서드이다. 메서드의 이름만 보아도 로또 객체를 자동으로 생성하는지,    
아니면 수동으로 생성하는지 단번에 이해할 수 있을 것이다.   
   
이처럼 정적 팩토리 메서드를 사용하면 해당 생성의 목적을 이름에 표현할 수 있어 가독성이 좋아지는 효과가 있다.

2. 호출할 때마다 새로운 객체를 생성할 필요가 없다.
enum과 같이 자주 사용되는 요소의 개수가 정해져있다면 해당 개수만큼 미리 생성해놓고 조회(캐싱)할 수 있는 구조로 만들수 있다.    
정적 팩터리 메서드와 캐싱구조를 함께 사용하면 매번 새로운 객체를 생성할 필요가 없어진다.

```java
public class LottoNumber {
  private static final int MIN_LOTTO_NUMBER = 1;
  private static final int MAX_LOTTO_NUMBER = 45;

  private static Map<Integer, LottoNumber> lottoNumberCache = new HashMap<>();

  static {
    IntStream.range(MIN_LOTTO_NUMBER, MAX_LOTTO_NUMBER)
                .forEach(i -> lottoNumberCache.put(i, new LottoNumber(i)));
  }

  private int number;

  private LottoNumber(int number) {
    this.number = number;
  }

  public LottoNumber of(int number) {  // LottoNumber를 반환하는 정적 팩토리 메서드
    return lottoNumberCache.get(number);
  }

  ...
}
```
객체의 캐싱을 통해서 새로운 객체 생성의 부담을 덜 수 있다는 장점도 있지만, 생성자의 접근 제한자를 private으로 설정함으로써.  
객체 생성을 정적 팩토리 메서드로만 가능하도록 제한할 수 있다는 것이다. 이를 통해 정해진 범위를 벗어나는 로또 번호의 생성을 막을 수 있다는 장점을 확보할 수 있다.

3. 하위 자료형 객체를 반환할 수 있다.
하위 자료형 객체를 반환하는 정적 팩토리 메서드의 특징은 상속을 사용할 때 확인할 수 있다. 이는 생성자의 역할을 하는 정적 팩토리 메서드가 반환값을 가지고 있기 때문에 가능한 특징이다.

Basic, Intermediate, Advanced 클래스가 Level라는 상위 타입을 상속받고 있는 구조를 생각.     
시험 점수에 따라 결정되는하위 등급 타입을 반환하는 정적 팩토리 메서드를 만들면, 다음과 같이 분기처리를 통해 하위 타입의 객체를 반환할 수 있다.
```java
public class Level {
  ...
  public static Level of(int score) {
    if (score < 50) {
      return new Basic();
    } else if (score < 80) {
      return new Intermediate();
    } else {
      return new Advanced();
    }
  }
  ...
}
```

4. 객체 생성을 캡슐화 할 수 있다.
DTO와 Entity간에는 자유롭게 형 변환이 가능해야 하는데, 정적 팩터리 메서드를 사용하면 내부 구현을 모르더라도 쉽게 변환할 수 있다.

```java
public class CarDto {
  private String name;
  private int position;

  pulbic static CarDto from(Car car) {
    return new CarDto(car.getName(), car.getPosition());
  }
}


// Car -> CatDto 로 변환
CarDto carDto = CarDto.from(car);
```

```java
Car carDto = CarDto.from(car); // 정적 팩토리 메서드를 쓴 경우
CarDto carDto = new CarDto(car.getName(), car.getPosition); // 생성자를 쓴 경우
```


```java
abstract class Coffee { 
    public abstract int getPrice(); 
    
    @Override
    public String toString(){
        return "Hi this coffee is "+ this.getPrice();
    }
}

class CoffeeFactory { 
    public static Coffee getCoffee(String type, int price){
        if("Latte".equalsIgnoreCase(type)) return new Latte(price);
        else if("Americano".equalsIgnoreCase(type)) return new Americano(price);
        else{
            return new DefaultCoffee();
        } 
    }
}

class DefaultCoffee extends Coffee {
    private int price;

    public DefaultCoffee() {
        this.price = -1;
    }

    @Override
    public int getPrice() {
        return this.price;
    }
}

class Latte extends Coffee { 
    private int price; 
    
    public Latte(int price){
        this.price=price; 
    }
    @Override
    public int getPrice() {
        return this.price;
    } 
}

class Americano extends Coffee { 
    private int price; 
    
    public Americano(int price){
        this.price=price; 
    }
    @Override
    public int getPrice() {
        return this.price;
    } 
} 

public class HelloWorld{ 
     public static void main(String []args){ 
        Coffee latte = CoffeeFactory.getCoffee("Latte", 4000);
        Coffee ame = CoffeeFactory.getCoffee("Americano",3000); 
        System.out.println("Factory latte ::"+latte);
        System.out.println("Factory ame ::"+ame); 
     }
} 

/*
Factory latte ::Hi this coffee is 4000
Factory ame ::Hi this coffee is 3000
*/

```
- CoffeFactory 라는 상위 클래스가 중요한 뼈대를 결정하고 하위 클래스인 LatteFactory 가 구체적인 내용을 결정하고 있습니다. 이는 의존성 주입이라고도 볼 수 있습니다.
CoffeFactory 에서 LatteFactory 의 인스턴스를 생성하는 것이 아닌 LatteFactory 에서 생성한 인스턴스를 CoffeFactory 에 주입하고 있기 때문이다.
또한 CoffeFactory 를 보면 static 으로 getCoffe() 정적 메서드를 정의한 것을 알 수 있는데, 정적 메서드를 쓰면 클래스의 인스턴스 없이 호출이 가능하며
메모리를 절약 할 수 있고 인스턴스에 묶이지 않는다. 

출처 : https://tecoble.techcourse.co.kr/post/2020-05-26-static-factory-method/ , 면접을 위한 CS 전공지식
