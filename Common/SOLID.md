## SOLID (객체지향 설계 5원칙)

#### 1. SRP(Single Responsibility Principle) 단일 책임 원칙
- 모든 클래스는 각각 하나의 기능만 가져야 한다는 의미  
- 해당 클래스가 제공하는 모든 서비스는 단 하나의 책임을 수행 하는데 집중 되어야 한다는 원칙이다.  
- SRP 원칙을 적용함으로 클래스간의 영향을 줄일 수 있으며, 응집도는 높이고 결합도는 낮출 수 있다.
#### 2. OCP(Open Closed Principle) 개방 폐쇄 원칙
- 소프트웨어의 모든 구성요소(클래스, 모듈, 메서드)는 확장에는 열려있고, 변경에는 닫혀 있어야 한다는 원칙이다.
- 요구사항의 변경이나 추가사항이 발생하더라도 기존 구성요소는 수정이 일어나지 말아야 하며 쉽게 확장이 가능하고 재사용할 수 있어야 한다는 뜻이다.
- 로버트 마틴은 OCP는 관리가 용이하고 재사용 가능한 코드를 만드는 기반이며, OCP를 가능케 하는 중요한 매커니즘은 추상화와 다형성이라고 설명한다.
- 클래스를 설계 할 때 변할 부분과 변하지 않을 부분을 명확히 구분해야 한다.  
변할 수 있는 부분은 추상화하여 상속하는 클래스가 의존할 수 있게 코드를 작성해야 한다.
```
interface Car {
    public int acceleration(int speed);
}

class HyundaiCar implements Car {
    private int defaultSpeed;
    
    @override
    public int accelration(int speed) {
        return defaultSpeed + speed;
    }
    
    public void info() {
        system.out.println("hyundai");
    }
}
```

위 코드와 같이 interface를 통해서 변해야 할 부분은 override를 통해 열어두고 변하지 않아야할 부분은 닫아 두게 할 수 있다.
#### 3. LSP(Liskov Substitution Principle) 리스코프 치환 원칙
- LSP는 자식 클래스는 부모 클래스에서 가능한 행위를 수행 할 수 있어야 한다는 의미이다.
- 한번에 이해하기 어려운 내용처럼 느껴지나 쉽게 풀이하자면 서브 클래스가 부모 클래스를 상속하게 되었을 때 부모가 가진 기능을 재정의 하거나 추가적인 기능을 통해  
부모의 상태를 변경하지 말아야 한다는 뜻이다.
- 서브 클래스가 슈퍼 클래스의 책임을 무시하거나 재정의 하지 않고 확장만 수행한다는 것을 의미한다.
#### 4. ISP(Interface Segregation Principle) 인터페이스 분리 원칙
- 인터페이스 분리 원칙은 클라이언트에서는 클라이언트 자신이 이용하지 않는 기능은 구현하지 말아야 한다.  
하나의 일반적인 인터페이스보다는 여러 개의 구체적인 인터페이스가 낫다는 원칙이다.
- 예를 들어 스마트폰의 기능중 전화, 웹서핑, 사진 촬영 등 다양한 기능을 사용할 수 있다.  
그런데 전화를 할 때 웹서핑, 사진촬영등 다른기능을 함께 사용하지는 않는다.  
그렇게 때문에 전화기의 각 기능은 서로 다른 인터페이스로 구현하여 영향을 주지 않도록 설계 해야 한다는 뜻이다.
#### 5. DIP(Dependency Inversion Principle) 의존관계 역전 원칙
- 객체지향 프로그래밍에서 객체는 서로 도움을 주고 받으며 의존 관계를 발생시킨다.  
  DIP는 의존 관계를 맺을 때 변화하기 쉬운 것 또는 자주 변화하는 것보다는 변화하기 어려운 것, 거의 변화가 없는 것에 의존하라는 원칙이다.
- DIP를 만족하려면 어떤 클래스가 도움을 받을 때 혹은 의존할 때 구체적인 클래스는 변화할 확률이 높기 때문에 이를 추상화한 인터페이스나 추상 클래스와 의존관계를 맺도록 설계 해야 한다.
```
public interface Keyboard {
    void info();
    void keyPress();
}

public class SuperKeyboard implements Keyboard {
    private String keyboardName;
    
    @override
    void info() {
        system.out.println(keyboardName);
    }
    
    @override
    void keyPress() {
        system.out.println("press");
    }
}

public class Computer {
    private Keyboard keyboard;
    
    Computer(Keybaord keyboard) {
        this.keyboard = keyboard;
    }
}

public class main {
    public static void main(String[] args) {
        Keybaord keyboard = new SuperKeyboard();
        Computer computer(keyboard);
    }
}
```

위 코드를 보면 Computer 클래스 객체 생성시 SuperKeyboard를 직접 주입하는 것이 아닌 Keyboard interface를 주입하고 있다.  
추후 keyboard를 다른 keyboard를 교체하게 되더라도 Computer 클래스에는 영향을 미치지 않게 된다.  
이 부분이 DIP가 추구하고자 하는 원칙이다.  
