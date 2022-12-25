### Builder Pattern(빌더)
- 빌더 패턴은 디자인 패턴중 생성 패턴에 해당된다.
- 복잡한 객체의 생성 과정과 표현 방법을 분리하여 동일한 생성 절차에서 서로 다른 표현 결과를 만들 수 있게 하는 패턴
- 빌더 패턴을 통하여 복합 객체의 생성 과정을 좀더 가독성있고 유연하게 만들 수 있다.
- 예를 들어 Java의 경우 객체 생성시 생성자로 넘겨야 할 파라미터의 갯수가 많을 경우 가독성이 심하게 떨어지는 단점이 있다.
```
// 매개변수의 의미, 각각의 위치등이 한번에 파악하기 어렵다
Factory factory = new Factory("abc", 1, seoul);
```
빌더 패턴을 통하여 각각의 파라미터가 어떤 인자와 매핑 되는지 확인할 수 있으며, 파라미터의 순서가 바뀌어도 영향을 받지 않는다.

```aidl
Factory factory = Factory.builder()
                    .name("abc")
                    .factoryNumber(1)
                    .location(seoul)
```
위와 같이 빌더 패턴을 통해 객체 생성시 기존 생성자 방식과 비교하여 가독성이 좋아진 것을 확인할 수 있다.

**빌더 패턴 구현**

```aidl
Class Factory{
    private String name;
    private Long factoryNumber;
    private Location location;
    
    private Factory(Builder builder) {
        this.name = builder.name;
        this.factoryNumber = builder.factoryNumber;
        this.location = builder.location;
    }
    
    public static class Builder {
        //필수 매개 변수
        private String name;
        //선택 매개 변수
        private Long factoryNumber = 0;
        private Location location = seoul;
        
        public Builder(String name) {
            this.name = name;
        }
        
        public Builder factoryNumber(Long factoryNumber) {
            this.factoryNumber = factoryNumber;
        }
        
        public Builder location(Location location) {
            this.location = location;
        }
        
         public Factory build() {
            return new Factory(this);
        }
    }
}
```

