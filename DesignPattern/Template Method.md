### Template Method(템플릿 메서드)

주말에 일어나 게임 할때를 생각해보자.  
1. 컴퓨터를 킨다.
2. 게임을 킨다.
3. 즐긴다.
4. 컴퓨터를 끈다.

이것을 코드로 나타내려 고민할때 어떤 문제가 발생할까?  
여기서 매일 어떤 게임을 할지 달라지는 문제가 있다.  
 이럴때 나머지 동작은 같지만 특정 부분의 동작에 변화를 줘야할때 사용하는 것이 템플릿 메서드 패턴이다  

**Template Method?**
- 템플릿 메소드 패턴은 여러 작업들이 완전히 동일한 단계를 갖지만 일부 동작은 각각 다르게 구현해야 할 때 사용된다. (아래와 같은 두가지로 나뉨)
  - 실행 과정을 구현한 상위 클래스
  - 실행 과정의 일부 단계를 구현한 하위 클래스
- 여기서 상위 클래스는 작업의 전체 흐름을 구현한다 (일어나고, 씻고, 대중교통 타고..) 
- 하위 클래스는 추상 클래스를 통해 구현한다.

```
abstract public class Game {
    public void play() {
        System.out.println("컴퓨터를 킨다.");
        getGame();
        System.out.println("즐긴다.");
        System.out.println("컴퓨터를 끈다.");
    }
    
    protected abstract void getGame();
}

public class Lol extends Game {
    @Override
    protected void getGame() {
        System.out.println("롤을 킨다");
    }
}

public class BattleGround extends Game {
    @Override
    protected void getGame() {
        System.out.println("배그를 킨다");
    }
}
```

Game 추상 클래스는 공통된 부분을 play()에 구현해놓았다.  
게임의 종류에 해당 하는 부분을 getGame()이라는 추상 메서드로 분리해놓았다.  
이렇게 템플릿 메서드를 통해서 불필요한 중복을 제거할 수 있다.