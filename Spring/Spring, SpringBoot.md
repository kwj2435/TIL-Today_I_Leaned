### Spring과 SpringBoot의 차이  
1. Spring
   1. Spring은 Java 기반의 오픈 소스 프레임워크
   * 프레임워크란?
     * 개발을 수월하게 하기 위해 제공된 소프트웨어 개발 환경이며 라이브러리는 사용자가 필요한 시점에 해당 기능의 라이브러리를 추가하지만  
     프레임워크의 경우 프레임워크가 정해놓은 틀안에서 개발이 진행되며 개발에 필요한 관련 기능(git, di, aop)등을 기본적으로 탑재하고 있다.
2. Spring Boot
   1. Embedded Tomcat 사용으로 별도의 Tomcat을 설치하거나 버전관리를 해줘야 하는 수고가 없다.
   2. Spring FrameWork 에서는 dependency들간의 호환을 신경쓰고 관리해줘야 했으나 boot의 경우 starter 팩을 지원 해줌으로 대부분의 dependency 관리 걱정을 덜게 되었다.
   3. properties, yml 파일을 통해 Spring에서 필요로 하는 설정을 AutoConfiguration으로 적용할 수 있다.