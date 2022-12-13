### IOC(Inversion Of Controll)  
IOC라는 용어는 Spring에서만 사용되는 것이 아닌 객체지향 전반에 걸쳐 사용되는 디자인 패턴적 용어이다.
결과적으로 객체간의 강한 결합을 줄이기 위한 하나의 디자인 패턴을 의미한다.
1. Spring의 IOC  
   1. Spring 에서는 인스턴스의 생성과 의존 관계 설정, 사용, 제거 등의 작업을 코드 대신 Spring Container가 담당한다.  
   이를 가르켜 스프링에서 코드 대신 인스턴스에 대한 제어권을 갖고 있다 하여 IOC 즉 제어의 역전이라 부른다.  
   따라서 스프링 컨테이너를 IOC 컨테이너라고도 부른다.


2. Spring Container의 종류
   1. Bean Factory
      1. Spring Container의 최상위 인터페이스.
      2. Spring Bean을 관리하고 조회하는 역할을 담당한다.
      3. getBean Method를 제공한다.
      4. Bean에 대한 전반적인 기능을 제공한다.
   2. ApplicationContext
      1. BeanFactory의 기능을 상속 받아 제공한다.
      2. Bean에 대한 기능만을 담당한 BeanFactory와 달리 ApplicationContext는 여러 부가기능을 제공한다.  
      에를 들어 ApplicationContext는 MessageSource, ResourceLoader 등의 인터페이스를 상속 받고 있는데 각각의 인터페이스를 통해  
      메시지 소스를 통한 국제화 기능, 파일, 클래스패스, 외부 등의 리소스를 편리하게 조회하는 기능을 제공한다.


3. IOC와 DI와의 관계
    1. DI는 객체의 의존성을 외부에서 주입받게 되는 것을 의미하는데, 여기서 외부의 역할을 Spring에서는 SpringContainer가 담당하게 된다.
4. Spring의 빈 생성 방식
   1. Spring은 기본적으로 별다른 설정이 없을 경우 내부에서 생성하는 빈 인스턴스를 모두 싱글톤으로 생성한다.
   2. Spring은 @Component 어노테이션을 명시한 클래스들을 컴포넌트 스캔을 통하여 Bean으로 등록한다.
   3. 혹은 @Bean 어노테이션을 선언한 메서드의 return 인스턴스를 이용해 직접 등록할 수도 있다.