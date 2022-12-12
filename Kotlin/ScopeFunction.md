코틀린 표준 라이브러리에는 객체 컨텍스트 안에서 코드 블록을 실행하는 데 도움이 되는 여러 함수가 있다.  
람다식을 써서 객체에서 이런 함수를 호출하면 임시 범위가 만들어진다. 이런 기능을 Scope Functions 라고 한다.  

Scope Function 을 통해 해당 객체에 어떤 함수 혹은 로직들이 적용되는지 알기 쉬위며 이를 통해 가독성이 향상 된다.

Scope Function 적용 전
```
val alice = Person("Alice", 20, "Amsterdam")
println(alice)
alice.moveTo("London")
alice.incrementAge()
println(alice)
```
Scope Function 적용 후
```
Person("Alice", 20, "Amsterdam").let {
    println(it)
    it.moveTo("London")
    it.incrementAge()
    println(it)
}
```

Scope Function의 종류 (apply, also, let, with, run)
- apply  
  apply는 객체를 설정하는 상황에서 사용된다. apply는 객체 자신을 다시 반환하기 때문에 특정 객체의 프로퍼티를 설정후 바로 사용하기 쉽다.  
```
val adam = Person("Adam").apply {
    age = 32
    city = "London"        
}
```
- also  
  also는 객체의 속성을 전혀 사용하지 않거나 이를 변경하지 않으면서 사용하는 경우에 사용된다.  
대표적으로 객체의 데이터 유효성을 확인하거나, 디버그, 로깅 등의 부가적인 목적으로 사용할 때에 적합하다.  
also는 receiver로 받은 객체를 it으로 사용할 수 있으나, 받은 객체를 그대로 반환한다(변경X)
```
val numbers = mutableListOf("one", "two", "three")
numbers
    .also { println("The list elements before adding new one: $it") }
    .add("four")
```
- let  
let은 call chain의 결과에서 1개 혹은 그 이상의 함수를 호출하는 데 사용할 수 있다.
```
val numbers = mutableListOf("one", "two", "three", "four", "five")
val resultList = numbers.map { it.length }.filter { it > 3 }
println(resultList)
```
위의 코드는 아래와 같이 변경이 가능하다.
```
val numbers = mutableListOf("one", "two", "three", "four", "five")
numbers.map { it.length }.filter { it > 3 }.let { 
    println(it)
    // and more function calls if needed
} 
```
- with  
with 함수는 2개의 인자를 사용하게 된다. 첫번째는 수신객체이고 두번째는 첫번째로 받은 수신객체를 인자로 하는 람다 함수이다.  
다음과 같은 상황에서 사용된다.
```
fun alphabet(): String {
    val result = StringBuilder()
    for (letter in 'A'..'Z') {
        result.append(letter)
    }
    result.append("\nNow I Know the alphabet!")
    return result.toString()
}

```
위 코드는 StringBuilder를 result 변수에 담고 반복문 로직을 호출.. 등등의 로직이 구현되어 있다.
해당 코드를 with를 사용하여 구현시 좀더 가독성 있는 코드를 만들 수 있다.
```
fun alphabet() = with(StringBuilder()) {
    for (letter in 'A'..'Z') {
        append(letter)
    }
    append("\nNow I Know the alphabet!")
    toString()
}
```
- run  
apply와 비슷하지만 이미 생성된 객체에 대한 call chain으로 호출한다는 점이 다르다.  
apply는 호출 객체를 it을 통해 접근하지만 run은 scope 블럭 내에서 이미 호출함수를 전제하고 있음
```
val service = MultiportService("https://example.kotlinlang.org", 80)

val result = service.run {
    port = 8080
    query(prepareRequest() + " to port $port")
}

// the same code written with let() function:
val letResult = service.let {
    it.port = 8080
    it.query(it.prepareRequest() + " to port ${it.port}")
}
```