## 추상 클래스와 인터페이스

### 추상 클래스

클래스를 설계도라 하면, 추상 클래스는 **미완성 설계도**에 비유할 수 있다.  
(여기서 클래스가 미완성이라는 것은 추상 메서드를 포함하고 있다는 의미이다.)

**추상 메서드**
선언부만 작성하고 구현부는 작성하지 않은 채로 남겨 둔 것이 추상메서드다.  
추상 메서드는 상속받는 클래스에 따라 달라질 수 있다.

### 추상 클래스 규칙
- 추상 클래스는 키워드 `abstract`를 붙여 표현한다.
  추상 메서드를 포함하지 않는 클래스에서도 `abstract`를 붙여서 추상 클래스로 지정할 수도 있다.
- 클래스를 abstract로 지정하면 `new`를 통해 객체를 직접 생성할 수 없다.
- 메소드에 abstract를 사용할 경우 interface의 메소드와 같이 구현 부분은 없다.
- abstract로 선언한 메소드를 자식 클래스에서 반드시 구현해야 한다.(오버라이딩)  
  이는 자식 클래스에서 추상 메서드를 반드시 구현하도록 강제하는 것이다.


### example
```java
public abstract class Player{
  boolean pause;
  int currentPos;
  
  public Player(){
    this.pause = false;
    this.currentPos = 0;
  }
  //지정된 위치에서 재생을 시작하는 기능 수행되도록 작성
  abstract void play(int pos);
  //재생을 즉시 멈추는 기능을 수행하도록 작성
  abstract void stop();
  
  void pause(){
    if(pause){
      pause= false;
      play(currentPos);
    }else{
      pause= true;
      stop();
    }    
  }  
}
```

Player 추상 클래스는  
VCR이나 Audio 같은 재생이 가능한 기기의 부모 클래스가 될 수 있다.  
이제 Player 추상 클래스를 상속받는 CDPlayer 클래스를 만들어보자.

```java
public class CDPlayer extends Player{
 @Override
 void play(int pos){
  //구현 생략
 }
 
 @Override
 void stop(){
  //구현 생략
 }
 
 //CDPlayer 클래스에 추가로 정의된 멤버
  int currentTrack;

  void nextTrack() {
      currentTrack++;
      // ...
  }

  void preTrack() {
      if (currentTrack > 1) {
          currentTrack--;
      }
      // ...
  }
 
```

부모 클래스의 추상메서드를 CDPlayer에 맞게 오버라이딩해주고,  
CDPlayer만의 새로운 멤버들을 추가해주었다.
