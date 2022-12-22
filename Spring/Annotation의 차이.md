#### @Component, @Service, @Repository, @Controller, @RestController의 차이
어노테이션은 Java 5 부터 추가된 문법 요소로, 코드 사이에 주석처럼 쓰이며, 실제 데이터를 의미하는 것이 아닌 데이터를 위한 데이터 즉 메타데이터를 의미한다.
1. @Component
- Component 어노테이션은 특정 클래스를 Bean으로 등록하기 위한 어노테이션이다.
- 상속관계에 있는 어노테이션중 가장 최상단의 루트 어노테이션이다.
- 추가로 @Bean 어노테이션의 경우 개발자가 직접 제어가 불가능한 외부 라이브러리 등을 Bean으로 등록하기 위해 사용된다.
2. @Service
- 비즈니스 로직을 구현하는 클래스에 사용되며 MVC패턴에서는 서비스 레이어를 의미한다.
- @Component와 기능상의 차이는 없으나, 레이어 구분을 하기위해 사용된다.
4. @Repository
- Data Access Layer에 사용된다.
- Service 어노테이션과 마찬가지로 해당 클래스가 Repository Layer를 의미함을 명시적으로 알려준다.
6. @Controller
- 해당 클래스가 Controller Layer의 역할을 한다는 정보를 스프링에게 알려주며 해당 어노테이션이 적용된 클래스에서 @RequestMapping과 같은 부가 어노테이션을  
사용할 수 있다.
- @Controller 어노테이션을 사용한 클래스의 메서드에서 리턴되는 String Response는 DispatcherServlet의 ViewResolver에게 전달되며 ViewResolver는 해당 정보  
를 통해 알맞은 View를 찾아 클라이언트에게 전달하게 된다.
8. @RestController
- Controller 어노테이션과 동일한 기능을 가지나 해당 클래스가 가지는 멤버 메서드의 리턴값의 처리 방식이 다르다.
- Controller는 메서드의 return 값을 viewResolver에서 처리하였으나, RestController의 경우 JsonParser가 Return값을 처리하게 된다.
- 결과적으로 스프링에서 기본으로 적용한 혹은 사용자가 임의로 정한 JsonParser 규칙에 따라 데이터가 변환되어 사용자에게 전달되게 된다.