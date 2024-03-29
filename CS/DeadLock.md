## DeadLock (데드락, 교착상태)

프로세스가 자원을 얻지 못해 다음 처리를 하지 못하는 상태로, 교착 상태라고도 한다.  
시스템적으로 한정된 자원을 여러 곳에서 사용하려 할 때 발생한다.  

### 발생조건
데드락 발생의 간단한 예시  
T1 - 프로세스1이 리소스 1을 얻고, 프로세스 2는 리소스 2를 얻는다.
T2 - 프로세스1은 리소스 2를, 프로세스 2는 리소스1을 기다린다.  
서로가 서로의 자원을 기다리며 교착상태가 발생한다.

교착 상태는 한 시스템 내에서 아래의 네 조건이 성립할 때 발생한다.
1. 상호 배제(Mutual exclusion)
- 하나의 자원은 한번에 한 프로세스만이 사용할 수 있어야 한다.
2. 점유 대기(Hold and wait)
- 최소한 하나의 자원을 점유하고 있으면서 다른 프로세스에 할당되어 사용하고 있는 자원을 추가로 점유하기 위해 대기하는 프로세스가 존재 해야 한다.
- 내가 자원을 가지고 있으면서, 다른 자원을 기다리는 상태를 의미
3. 비선점(No preemption)
- 다른 프로세스에 할당된 자원은 사용이 끝날 때 까지 강제로 뺏을 수 없다.
4. 순환 대기(Circular wait)
- 프로세스의 집합에서 순환 형태로 자원을 대기하고 있어야 한다.
- 위 교착 상태의 예시

### 해결 방법
#### 예방
- 상호 배제 부정
  - 여러 개의 프로세스가 공유 자원을 사용할 수 있도록 한다.
- 점유 대기 부정
  - 프로세스가 실행되기 전 필요한 모든 자원을 할당한다.
- 비선점 부정
  - 자원을 점유하고 있는 프로세스가 다른 자원을 요구할 때 점유하고 있는 자원을 반납하고 요구한 자원을 사용하기 위해 기다린다.
- 순환 대기 부정
  - 자원에 고유 번호를 부여하고 번 호 순서대로 자원을 요구하도록 한다.
#### 회피
교착 상태 발생시 피해가는 방법
- 은행원 알고리즘
  - 다이직스트라 알고리즘을 개발한 Edsger Dijkstra가 개발 한 알고리즘으로 '최소한 고객 한명에게 대출해줄 금액은 항상 은행이 보유해야 한다'  
  라는 개념에서 착안한 알고리즘이다.
  - 자원을 요청할 때 safe 상태를 유지하는 경우 할당한다, 즉 총 요청 자원의 수가 남은 자원의 수보다 적은 프로세스만 선택하여 수행한다.
#### 탐지
교착 상태 탐지는 회복과 함께 움직인다.  
교착 상태 탐지 알고리즘을 통해 현재 시스템에 교착상태가 있는지 주기적으로 확인하며, 교착상태 발생시 회복 알고리즘을 통해 교착 상태를 해결한다.  
다만 탐지 알고리즘을 주기적으로 실행하기 때문에 시스템 성능에 부하를 주게 된다.  
#### 회복
교착 상태를 회복하는 방법은 프로세스 강제 종료와 자원 선점 두가지 방법이 있다.
- 프로세스 종료
- 자원 선점
  - 희생 프로세스 선정
  - 롤백
  - 기아 현상
    - 우선 순위의 기준에 따라 희생하는 프로세스만 계속 희생될 수 있다. 선점 횟수에 가중치를 부여해 선점이 많이 된 프로세스에게 우선권을 주는 방식으로 해결할 수 있다.