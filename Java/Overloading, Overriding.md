오버로딩(Overloading)
- 같은 이름의 메서드 여러개를 가지면서 매개변수의 유형과 갯수가 다르도록 하는 것
```
    void dog(){
        System.out.println("매개변수 없음");
    }
    
    void dog(int a, int b){
        System.out.println("매개변수 :"+a+", "+b);
    }
    
    void dog(String c){
        System.out.println("매개변수 : "+ c);
    }

```
오버라이딩(Overriding)
- 상위 클래스에 정의되어 있는 메서드를 하위 클래스에서 재정의 하여 사용하는 것
```
    class Humen {
        public int age;
        
        public void info() {
            System.out.println("my age"+ age);
        }
    }
    
    class Docter extends Human {
        public String name;
        
        override public void info() {
            System.out.println(super.age +" "+:name);
        }
    }
```