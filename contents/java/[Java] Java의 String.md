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
- `equals()` 메소드의 수행 결과는 true다. 이는 문자열 내용을 비교하기 때문에 같은 문자열에 대해서 true를 반환하는 것이 맞다.


### 왜 이런 결과가 나올까?

이를 위해서는 동작 방식에 대한 이해가 필요하다. 
String을 리터럴로 선언할 경우, 내부적으로 String의 `intern()`이라는 메소드가 호출되게 된다.

- `intern()` : 주어진 문자열이 **String Constant Pool**에 존재하는지 검색하고 있다면 그 주소값을 반환하고
              없다면 **String Constant Pool**에 넣고 새로운 주소값을 반환하게 된다.
              

```java
public class StringMemoryInternTest{
  public static void main(Strig[] args){
  
    String literal = "loper";
    String object = new String("looper");
    String intern = object.intern(); //명시적으로 호출.
    
    literal == object; //false
    literal.equals(object) //true
    
    literal == intern; //true
    
  }
}
```

기존에 `new`를 통해 생성된 **String**객체와 리터럴로 생성된 **String** 객체를 `==`연산했을 경우, **false**를 반환했지만,
`new`를 통해 생성된 **String** 객체의 `intern()`메소드를 호출하여 새로운 String 객체인 intern에 대입할 경우,
리터럴로 생성된 String 객체와 `==` 연산시 **true**를 반환하게 된다. 

리터럴로 **looper**라는 문자열이 **String Constant Pool**에 저장되었고, 
`intern()`메소드를 호출하면서 **String Constant Pool**에 "**loper**"라는 문자열을 검색하게 되고 이미 저장된 "**loper**" 문자열을 발견할테니 동일한 주소값을 반환하게 되므로 **true가** 성립되는 것이다.
