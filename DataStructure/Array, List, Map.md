###Array, List, Map

1. **Array**
- 인덱스의 개념을 가지고 있어 해당 인덱스를 가지고 데이터에 바로 접근 할 수 있다.
- 데이터 조회에서는 O(1)로 높은 성능을 가지나, 삽입 삭제에서는 O(N)으로 낮은 성능을 가진다.
- 한번 선언한 배열의 크기는 임의로 바꿀 수 없다. (고정된 크기를 갖는다.)
- 데이터 갯수가 확실하게 정해져 있으며, 접근이 빈번한 경우 효율적인 자료구조이다.

```aidl
//Java
int[] arr = new int[10];

//Kotlin
val arr = IntArray(10)
val arr = intArrayOf(1,2,3)
```
2. **List**
- 배열과 달리 인덱스의 개념이 없으며 특정 원소를 찾기 위해서는 순차탐색을 진행해야한다.
- 순차탐색으로 인해 조회시의 시간복잡도는 O(N)이지만 삽입, 삭제시 O(1)의 시간 복잡도를 가진다.
- 배열과 달리 크기가 고정적이지 않다. (삽입, 삭제에 유연하다)
- 각 노드가 이전, 이후 노드를 바라보고 있어 삽입, 삭제시 전후 노드의 참조 관계만을 바꿔주면 된다.(성능상 이점)
- Java의 경우 ArrayList, LinkedList 구현체가 존재한다.
```aidl
//Java
List<Integer> arr = new LinkedList<Integer>();
//Kotlin
val arr = mutableListOf<Int>();
```
3. **Map**
- key, value의 형태로 구성된 자료구조이다.
- key 값은 중복되지 않는다. 또한 인덱스의 개념이 없어 iterator를 이용해 순차탐색을 진행해야한다.
- HashMap, LinkedHashMap, TreeMap 구현체가 존재한다.
- HashMap의 경우 key에 대한 중복이 없으며 순서를 보장하지 않는다.  
또한 동기화가 보장되지 않으며 key와 value값으로 null 을 허용한다.
- LinkedHashMap은 입력된 순서를 보장한다.
- TreeMap은 이진 탐색 트리를 기반으로 키와 값을 저장하며, key 값을 기준으로 오름차순 정렬되고 빠른 검색이 가능하다. 다만 저장시 정렬로 인한 시간이 걸린다.