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


### 인터페이스
인터페이스는 일종의 추상 클래스로,  
추상메서드를 갖지만 추상 클래스보다 추상화 정도가 높아  
추상 클래스와 달리 몸통을 갖춘 일반 메서드, 멤버 변수를 구성원으로 가질 수 없다.   
추상 클래스를 미완성 설계도라 하면, 인터페이스는 구현된 것은 아무것도 없는,  
밑그림만 그려진 **기본 설계도** 라고 할 수 있다.

### 인터페이스 규칙
- 추상 클래스처럼 불완전한 것이기 때문에 그 자체만으로 사용되기 보다,  
  다른 클래스를 작성하는데 도움을 줄 목적으로 작성된다.
- 일반 메서드 또는 멤버 변수를 구성원으로 가질 수 없다.
- 모든 멤버 변수는 `public static final` 이어야 하며, 이를 생략할 수 있다. 
- 모든 메서드는 `public abstract`이어야 하며, 이를 생력할 수 있다.  
  (단, JDK1.8부터 static 메서드와 default 메서드를 사용할 수 있다.)

#### public static final의 목적?
인터페이스 변수는 아무 인스턴스도 존재하지 않는 시점이기 때문에 스스로 초기화될 권한이 없다.  
따라서 `public static final`를 사용해 구현 객체의 같은 상태를 보장한다.

### 인터페이스의 다중 상속
인터페이스는 인터페이스로부터만 상속받을 수 있으며,  
클래스와 달리 다중 상속을 받는 것이 가능하다. 

```java
public interface Movable{
  void move(int x, int y);
}

interface Attackable{
  void attack(Unit u);
}

interfacce Fightable extends Movable, Attackable{
}
```

클래스의 상속과 마찬가지로 자식 인터페이스는 부모 인터페이스에 정의된 멤버 모두 상속받는다.

#### Tip
인터페이스명은 대부분 "~를 할 수 있는"의 의미인 `able`로 끝나는 것들이 많다고 한다.  
그 이유는 어떤 기능 또는 행위를 하는데 필요한 메서드를 제공한다는 의미를 강조하기 위해서다.
때문에 그 인터페이스를 구현하는 클래스는 "~를 할 수 있는" 능력을 갖추었다는 의미이기도 하다.


### 추상 클래스 VS 인터페이스

#### 접근자
인터페이스에서의 모든 변수는 `public static final`,  
모든 메소드는 `public abstract`이다.
하지만 추상 클래스에서는 `static`이나 `final`이 아닌 필드를 가질 수 있고,  
`public, protected, private` 모두 가질 수 있다.

#### 다중 상속 여부
인터페이스를 구현하는 클래스는 여러개 인터페이스를 함께 구현할 수 있다.  
하지만 자바에서는 다중 상속을 지원하지 않기 때문에 여러 추상 클래스를 상속할 수 없다. 

#### 사용의도
**추상 클래스**는 이를 상속할 각 객체들의 공통점을 찾아 추상화시켜 놓은 것으로,  
상속 관게를 타고 올라갔을때 같은 부모 클래스를 상속하며  
부모 클래스가 가진 기능들을 구현해야할 경우 사용한다.

**인터페이스**는 상속 관계를 타고 올라갔을 때  
다른 조상 클래스를 상속하더라도, 같은 기능이 필요한 경우 사용한다.
클래스와 별도로 구현 객체가 같은 동작을 한다는 것을 보장하기 위해 사용한다.

####example
![classinterface](https://user-images.githubusercontent.com/60098769/144167530-cc48559f-abc8-4e37-82d6-6978edb22544.png)

제일 부모 클래스인 Creature은 생물에 대한 Abstract Class이다.    
각 생물은 구분에 따라 Animal 또는 Plant를 상속한다.    
그리고 각각이 할 수 있는 추가적인 기능들을 인터페이스로 구현했다.    
 
Animal을 상속받는 Dog, Cat은 Plant와 다르게  
bark(짖다) 할 수 있으니 Barkable 인터페이스를 구현하였다.  

여기서 눈여겨 볼 것은 바로 Eatable인데,  
Eatable 인터페이스는 현재 상속 관계가 다른 Dog, Cat, FlyHellPlant에게  
공통적인 기능인 Eat 기능을 인터페이스를 사용함으로 같은 기능을 구현하도록 강제하고 있다.  

그러면 결국 이 4가지 클래스 모두 생물 클래스를 상속하고 있는데,  
생물 클래스에 eat이라는 추상 메서드를 만들면 안되는가?라고 생각할 수 있지만  
Plant를 상속받은 Rose는 eat 메소드를 가질 수 없다.  

그러면 어떻게하지 🤷‍♀️  

이때 바로 인터페이스로 따로 선언을 해주어 각각 eat을 할 수 있는  
클래스에 implements해주어 만들어 주면 가독성이 올라가며 유지보수 또한 쉬워진다.  

### 추상클래스, 인터페이스 사옹 케이스 정리

#### 추상 클래스
- 관련성이 높은 클래스 간에 코드를 공유하고 싶은 경우
- 추상 클래스를 상속 받을 클래스들이 공통으로 가지는 메소드와 필드가 많거나,  
  public 이외의 접근자(protected, private)선언이 필요한 경우
- non-static, non-final 필드 선언이 필요한 경우 (각 인스턴스에서 상태 변경을 위한 메소드가 필요한 경우)

#### 인터페이스
- 서로 관련성이 없는 클래스들이 인터페이스를 구현하게 되는 경우.
- 특정 데이터 타입의 행동을 명시하고 싶은데, 어디서 그행동이 구현되는지는 신경쓰지 않는 경우.
- 다중 상속을 허용하고 싶은 경우

