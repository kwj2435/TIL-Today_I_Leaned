## Spring Container
스프링 컨테이너는 자바 객체의 생명 주기를 관리하며, 생성된 자바 객체들에게 추가적인 기능을 제공하는 역할을 한다.  
여기서 언급하는 자바 객체는 Bean이라고 부르며 IOC, DI의 원리가 스프링 컨테이너에 적용된다.  

개발자는 new 연산자, 인터페이스 호출, 팩토리 호출 방식으로 객체를 생성하고 소멸시킬 수 있는데, 스프링 컨테이너가 이 역할을 대신해준다.  
즉 제어 흐름을 내부가 아닌 외부에서 관리하게 되는 것이다.  

### Spring Container의 종류
스프링 컨테이너는 BeanFactory와 Applicationcontext가 있다.  
- BeanFactory
  - BeanFactory는 빈을 등록하고 생성및 조회및 반환등의 Bean을 관리하는 역할을 한다.
- ApplicationContext
  - ApplicationContext는 BeanFactory및 객체 관리에 필요한 인터페이스를 다중 상속하고 있다.
  - ApplicationContext는 BeanFactory의 기능을 물려받으며 객체 관리에 필요한 국제화가 지원되는 텍스트 메시지 관리 및 이벤트 발생 알림등의 부가적인 기능을 가지고 있다.

BeanFactory와 ApplicationContext는 빈의 로딩시점에서도 차이를 가지고 있다.  
BeanFactory의 경우 Bean의 사용이 필요로 하는 시점에 객체를 생성하여 전달하는 방식인 반면 ApplicationContext는 미리 Bean을 모두 생성해두고 필요애 따라 전달하는 구조이다.
> https://steady-coding.tistory.com/459