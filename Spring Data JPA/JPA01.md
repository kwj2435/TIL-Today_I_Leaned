JPA - 자바 진역 ORM 표준

ORM(Object Relational Mapping) 객체 관계 매핑
객체와 관계형 데이터베이스의 데이터를 자동으로 매핑(연결)해주는 것을 의미

객체 지향 프로그래밍은 클래스(객체)를 사용하고, 관계형 데이터베이스는 테이블을 사용한다
객체 모델과 관계형 모델 간에 불일치가 존재한다.

ORM은 객체와 테이블 사이에서 매핑을 해준다.

JPA는 애플리케이션과 JDBC 사이에서 동작

JPA의 가장 중요한 2가지
- 객체와 관계형 데이터베이스 매핑
- 영속성 컨텍스트

영속성 컨텍스트
ㄴ 엔티티 매니저 팩토리에서 요청이 올때마다 엔티티 매니저를 만듬
ㄴ 영속성 컨텍스트는 '엔티티를 영구 저장하는 환경'
ㄴ 영속성 컨텍스트는 물리적인 공간이 아닌 논리적인 개념으로 JPA에서 데이터를 영속하게 되면 DB에 저장되는게 아닌
영속성 컨텍스트에 저장된다.
ㄴ 엔티티 매니저안에는 영속성 컨텍스트(persistenContext)가 존재한다.

엔티티의 생명 주기
ㄴ 비영속 - 영속성 컨텍스트와 전혀 관계가 없는 새로운 상태 (객체를 생성한 상태)
ㄴ 영속 - 영속성 컨텍스트에서 관리되는 상태
ㄴ 준영속 - 영속성 컨텍스트에서 저장되었다가 분리된 상태
ㄴ 삭제 - 삭제된 상태

JPA 사용시 데이터가 DB에 반영되는 시점은 트랜잭션이 커밋되는 시점이다.

영속성 컨텍스트의 이점
ㄴ 버퍼링과 캐싱이 가능하다 (Dirty Checking)
ㄴ 영속성 컨텍스트 안에는 1차 캐시, 쓰기 지연 SQL 저장소가 있다.
ㄴ 데이터 조회시 영속성 컨텍스트의 1차 캐시를 먼저 조회한다. 없을 경우 데이터베이스를 조회함
* 트랜잭션이 끝날때 영속성 컨텍스트도 삭제된다. 영속성 컨텍스트의 1차 캐시는 하나의 트랜잭션에서만 유효한 캐시이기 때문에
큰 성능 이점은 없다.
* 반면 2차캐시는 애플레케이션이 종료되기전까지 유지된다.
ㄴ 영속 엔티티의 동일성 보장 (자바 Collection 에서 데이터를 꺼냈을때도 주소값이 동일하듯..)

Dirty Checking(변경감지)
ㄴ commit 시점에 1차캐시안에서 엔티티와 스냅샷을 비교한다.
ㄴ 변경을 확인할 경우 Update Query를 쓰기 지연 SQL 저장소에 생성하고 반영한다.

플러시(flush) - 영속성 컨텍스트의 변경 내용을 DB에 반영