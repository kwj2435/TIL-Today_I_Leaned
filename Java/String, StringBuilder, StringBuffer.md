### String, StringBuilder, StringBuffer

**1. String**
- Java의 String은 불변 객체이다. 우리가 String 타입을 선언후 문자열을 할당하여 사용하게 되면 내부적으로는 char[] 배열 변수를 선언하여  
문자열을 저장하고 사용하게 된다. 알다시피 배열은 사이즈가 고정적이며 동적으로 조절이 안된다.  
- String은 연산자 오버라이딩을 통해 "ABC" + "DEF" 와 같은 연산 혹은 내부 함수를 통해 초기 할당 문자열을 수정할 수 있는 다양한 기능을 제공한다.  
 이를 통해 String이 가변객체가 아닌가 할 수 있지만 내부 로직을 확인해보면 기존 char[] 배열 변수를 삭제후 새로 생성하는 방식으로 사용하고 있는것을 확인할 수 있다.  
이를 String의 데이터 변환이 자주 일어날 경우 성능 저하로 이어진다는 것을 이해할 수 있다.
####
**2. StringBuilder**
- StringBuilder는 StringBuffer와 같이 내부적으로 Buffer 역할의 배열을 만들어두고 문자열을 다르게 된다.
####
**3. StringBuffer**
- StringBuffer는 이름과 같이 내부적으로 buffer를 가지고 있다. StringBuffer의 인스턴스를 생성할때는 적절한 길이의 char형 배열이 생성된다.  
이렇게 생성된 배열은 문자열을 저장하고 편집할때 사용하는 buffer가 된다.  
buffer의 크기를 넘는 String이 들어오게 될 경우 String Buffer는 내부적으로 버퍼의 길이를 늘리는 작업을 진행하게 된다.

**4. StringBuilder, StringBuffer의 차이**
- 두 개의 차이점은 동시성 제어에서의 차이점이 있다. StringBuffer의 경우 데이터에 대한 동시성 제어처리로 멀티 스레드 환경에서 상대적으로 안전한 연산을 수행할 수 있도록  
처리되어 있으나, StringBuilder의 경우 동시성 처리가 되어 있지 않다.
- 그럼 StringBuffer를 사용하면 되는 것이 아닌가? 하지만 동시성 제어는 상대적으로 많은 리소스를 필요로 하는 작업이기에 멀티스레드 환경이 아니라면 StringBuffer를  
사용하지 않는 것이 성능상 이점을 가져갈 수 있다.
####

**5. 정리**
- 변하지 않는 문자열을 String 사용이 적합하다.
- 문자열의 값이 변하는 경우, 멀티 스레드 환경 에서는 StringBuffer를 사용하는 것이 좋다.
- 문자열의 값이 변하며, 멀티 스레드 환경이 아닌 경우 StringBuilder를 사용하는 것이 좋다.

etc. 불변객체와 가변 객체  
가변 객체 - Java에서 클래스의 인서턴스 생성 이후 내부 상태가 변경 가능한 객체 ArrayList, HashMap, StringBuilder ...  
불변 객체 - 가변객체와 반대로 인스턴스 생성 이후 내부 상태를 변경할 수 없는 객체로 String 등이 존재 ..