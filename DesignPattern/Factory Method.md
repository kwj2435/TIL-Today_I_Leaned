## Factory Method(팩토리 메서드 패턴)

팩토리 메서드 패턴은 객체를 생성하기 위해 인터페이스를 만든다.  
어떤 클래스의 인스턴스를 만들지는 서브클래스에서 결정하도록 한다.  
팩토리 메서드를 이용하면 인스턴스를 만드는 일을 서브클래스로 미룰 수 있다.   

이런 것이 필요한 이유가 뭘까?  
어떤 피자가게에서 페퍼로니 피자만을 전문적으로 만들어서 팔고 있었다.  
장사가 너무 잘되서 불고기 피자를 추가 만들어서 팔고 싶은데 모든 작업이 그동안 페퍼로니 피자에만 맞추어져 있었다.  
모든 장비와 절차를 드러내고 페퍼로니 피자와 불고기 피자를 동시에 만들도록 작업을 해야하는 상황이다.  
뿐만 아니라 이후에는 불고기 피자뿐 아니라 하와이안 피자, 치즈 피자까지도 만들어야 할 수 있다고 한다.  

이런 상황에서 피자라는 객체를 필요에 따라 원하는 타입의 피자로 생성 할 수 있도록 하는 방법이 팩토리 메서드 패턴이다.  

팩토리 메서드 패턴을 사용하는 이유는 클래스의 생성과 사용의 처리로직을 분리하여 결합도를 낮추기 위한 것이다.  

### 팩토리 메소드 패턴 예제
```
public abstract class PizzaFactory {
    abstract Pizza create(PizzaType pizzaType);
}
```
```
public abstract class Pizza {
    abstract public String info();
}
```
// Pizza 클래스 상속 받는 각 피자 클래스 생략  
// Pizza enum 클래스 생략
```
public class SeoulPizza extends PizzaFactory {
    @Override
    public Pizza create(PizzaType pizzaType) {
        switch(pizzaType) {
            case Cheese:
                return new CheesePizza();
            case Pepperoni:
                return new PepperoniPizza();
            case Bulgogi:
                return new BulgogiPizza();
        }
    }
}
```
```
public class Main {
    public static void main(String[] args) {
        PizzaFactory pizzaFactory = new SeoulPizza();
        
        Pizza pizza = pizzaFactory.create(PizzaType.Cheese);
        Pizza pizza = pizzaFactory.create(PizzaType.Bulgogi);
    }
}
```

