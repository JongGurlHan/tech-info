## Java의 String에 관해서

Java에서 String은 굉장히 자주 사용되며, 두 가지 생성 방식이 있다.

1. new 연산자를 이용한 방식
2. 리터럴을 이용한 방식

이 두 가지 방식에는 큰 차이점이 존재한다.

new를 통해 String 객체를 생성하면 **Heap** 영억에 존재하게 된다. 

리터럴을 이용할 경우, **String Constant Pool** 이라는 영역에 존재하게 된다.

```java
public class StringMemory{
  public static void main(String[] args){
    
    String literal = "loper";
    String object = new String("loper");
    
    literal == object; //false
    literal.equals(object); //true
   }
}
```

- `==` 연산의 결과는 false다. == 연산자는 객체의 주소값을 비교하기 때문에 일반 객체처럼 Heap 영역에 생성된 String 객체와 
  리터럴을 이용해 String Constant Pool에 저장된 String 객체의 주소값은 다를 수 밖에 없다.
- 'equals()' 메소드의 수행 결과는 true다. 이는 문자열 내용을 비교하기 때문에 같은 문자열에 대해서 true를 반환하는 것이 맞다.

