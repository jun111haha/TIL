# 팩토리 메서드 패턴
1. 팩토리 메서드 패턴(Factory method pattern)은 객체지향 디자인 패턴이다. Factory method는 부모(상위) 클래스에 알려지지 않은 구체 클래스를 생성하는 패턴이며. 자식(하위) 클래스가 어떤 객체를 생성할지를 결정하도록 하는 패턴이기도 하다. 부모(상위) 클래스 코드에 구체 클래스 이름을 감추기 위한 방법으로도 사용한다.

2. 팩토리 패턴은 객체를 사용하는 코드에서 객체 생성 부분을 떼어내 추상화한 패턴이자 상속 관계에 있는 두 클래스에서 상위클래스가 중요한 뼈대를 결정하고, 하위 클래스에서 
객체 생성에 관한 구체적은 내용을 결정하는 패턴이다. 상위 클래스와 하위 클래스가 분리되기 때문에 느슨한 결합을 가지며 상위 클래스에서는 인스턴스 생성 방식에 대해 전혀 알 필요가 없기 때문에
더 많은 유연성을 갖게 된다. 그리고 객체 생성 로직이 떼어져 있기 때문에 코드를 리팩터링하더라도 한 곳만 고치면 되기 떄문에 유지 보수성이 증가.

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
