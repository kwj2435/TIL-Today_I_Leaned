## [NHN FORWARD 2021] Redis 야무지게 사용하기

### 1. Redis 캐시로 사용하기
- 캐시란 데이터의 원래 소스보다 더 빠르고 효율적으로 액세스할 수 있는 임시 데이터 저장소
- Redis는 단순한 key-value, 인 메모리 데이터 저장소이며 굉장히 빠른 속도의 장점이 있음
- 캐싱전략
  - 읽기 전략
    - Lazy Loading(캐시 히트가 이루어지지 않을 경우 DB에서 조회하여 데이터를 가져오는 방식)
    - Lazy Loading의 경우 캐시에 데이터가 없더라도 DB를 통해 가져오기 때문에 오류의 위험이 적다.  
    다만 캐시를 향하던 트래픽이 많을 경우 DB 부하로 이어질 수 있다.  
    이런 문제를 해결하기 위해 DB의 데이터를 Redis를 미리 옮겨두는 Cache Warming 작업이 필요하다.
  - 쓰기 전략
    - Write-Around (DB에 저장후 캐시 미스 발생시 DB 데이터를 가져오는 방식)
    - Write-Through (DB에 데이터 저장시 캐시에도 함께 저장)
### 2. Redis 데이터 타입 야무지게 활용하기
- Redis는 여러 자료구조를 제공하고 있으며 특정상황별로 유용하게 사용할 수 있음.
- Strings
  - 단순 증감 연산
- Bits
  - 데이터 저장공간 절약 가능
  - 정수로 된 데이터만 카운팅 가능
- HyperLogLogs
  - 대용량 데이터를 카운팅 할 때 적절
  - set과 비슷하지만 저장되는 용량은 매우 작음
- Lists
  - Message Queue 기능으로 활용할 수 있음
  - Blocking 기능을 이용해 Event Queue로 사용
- Streams
  - 로그를 저장하기 가장 적절한 자료구조
### 3. Redis에서 데이터를 영구 저장하려면?
- Redis는 인메모리 데이터 스토어로써 서버 재시작시 모든 데이터 유실
- Redis를 캐시 이외의 용도로 사용한다면 적절한 데이터 백업이 필요하다.
- AOF
  - 명령이 실행될 때 마다 해당 명령이 파일에 기록된다.
  - 장애 상황 직전까지의 모든 데이터가 보장되어야 할 경우에 사용 적절
- RDB
  - 저장당시의 메모리의 데이터 그대로 사진찍듯 저장한다 (스냅샷 방식)
  - 백업은 필요하지만 어느정도의 데이터 손실이 발생해도 괜찮은 경우 사용에 적절
- 가장 강력한 내구성이 필요할 경우 AOF RDB를 동시에 사용하도록 Redis진영에서 권장함
### 4. Redis 아키텍처 선택 노하우
- Replication
  - 단순한 복제 연결 구조
  - 비동기식 복제를 진행함
- Sentinel
  - sentinel 노드가 다른 노드를 감시하며 마스터 노드가 죽으면 replica 노드로 복구를 진행함
- Cluster
  - 데이터가 자동으로 여러 마스터 노드에 분산되어 저장됨
  - 모든 노드가 서로를 감시하며, 마스터 비정상 상태일 때 자동 페일오버를 진행함
### 5. Redis 활용 쿨팁
- Redis는 Single Thread로 동작함 -> keys * 커맨드 사용하지 말 것
- 변경하면 장애를 막을 수 있는 기본 설정값
  - STOP-WRITES-ON-BGSAVE-ERROR = NO
    - RDB 파일 저장 실패 시 redis로의 모든 write 불가능
  - MAXMEMORY-POLICY = ALLKEYS-LRU
    - redis를 캐시로 사용할 때 Expire Time 설정 권장
    - 메모리가 가득 찼을 때 MAXMEMORY-POLICY 정책에 의해 키 관리됨
      - noeviction(default) : 삭제 안함
      - volatile-lru
      - allkeys-lru : 모든 키에 대해 lru 방식으로 키를 삭제함 