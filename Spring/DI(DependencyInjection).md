### DI (Dependency Injection)  
의존 관계 주입이라고 하며, 어떤 객체가 사용하는 의존 객체를 객체 내부에서 만들어 사용하는 것이 아닌
주입 받아 사용하는 방법이다.

* 의존 관계란?  
"A가 B를 의존한다는 표현은 어떤 의미일까?"  
토비의 스프링에서는 정의하기를 '의존대상 B가 변하면, 그것이 A에 영향을 미친다'로 정의하고 있다.  

* 강한 결합  
객체 내부에서 다른 객체를 생성 하게 되면 강한 결합도를 가지게 된다.  
A 클래스 내부에서 B 객체를 직접 생성할 경우, B객체 수정시 A또한 함께 수정해야 한다.
* 느슨한 결합  
객체를 주입 받게 되면 외부에서 생성된 객체를 넘겨 받게 되는 것으로 이 경우 결합도를 낮출 수 있다.  
  (외부에서 객체의 주입으로 A클래스에 영향이 없음)

예를 들어 장난감 자동차의 배터리가 일체형이라면 자동차를 교체해야겠지만, 배터리를 분리 하여 교체할 수 있다면 배터리만 교체하면 된다.  

Spring 에서의 DI 3가지 방법
- 필드 주입(Field Injection)
  ```
    @Component
    public class SampleController {
        @Autowired
        private SampleService sampleService;
    }
  ```
  필드 주입의 장점은 '간단'하다는 것이다. 다만 필드 주입의 경우 권장하지 않는 방법이며 아래와 같은 단점이 있다.  
  아래에 설명할 생성자 주입과 다르게 필드 주입은 해당 변수를 final 즉 immutability하게 생성하지 못한다. 이는 객체의 불변성이 보장받지 못하게 된다.  
  또한 필드 주입은 순환 의존성 문제를 발생시킨다.  
  A Class가 B Class를 참조할 때 B Class가 다시 A Class를 참조할 경우 이를 순환 의존성이라고 한다.  
  필드주입은 Spring Container외에 외부에서 의존성을 주입할 수 있는 방법이 없다.  
  이는 객체간의 의존성은 줄일 수 있으나 Spring에 대한 의존성을 유발시키게 된다.  


- 수정자 주입(Setter Injection)
  ```
    @Component
    public class SampleController {
        private SampleService sampleService;

        @Autowired
        public void setSampleService(SampleService sampleService) {
            this.sampleService = sampleService;
        }
    }
  ```
  수정자 주입은 SetMethod를 통해 사용되게 된다. 이는 의존성 주입을 런타임 시점에 선택으로 할 수 있다.  
  다만 이는 구현체에 수정자 주입을 하지 않아도 객체가 생성된다는 것이며 수정자 주입을 통해 의존객체를 주입 받지 못한 객체를 사용할 경우  
NullPointerException이 발생되게 된다. 즉 주입이 필요한 객체가 주입 되지 않아도 객체를 생성할 수 있다는것이 문제로 남아 있다.  


- 생성자 주입(Constructor Inejction)  
``` 
@Component
public class SampleService {
    private SampleDAO sampleDAO;
 
    @Autowired
    public SampleService(SampleDAO sampleDAO) {
        this.sampleDAO = sampleDAO;
    }
}

@Component
public class SampleController {

	private final SampleService sampleService = new SampleService(new SampleDAO());
    
	...
}
```
위와 같이 객체 생성시점에 생성자를 통해 의존성을 주입받아 사용할 수 있다.  
현 시점 Spring에서 권장하는 방법이며 다음과 같은 장점이 있다.  
1. 사용자가 임의로 null값을 주입하지 않는한 NullPointerException은 발생하지 않는다.
2. final을 통해 객체의 불변성을 보장할 수 있다.
3. 컴파일 시점에 순환 의존성을 확인할 수 있다.
4. 필드주입과 달리 Spring에 의존적이지 않게 된다.