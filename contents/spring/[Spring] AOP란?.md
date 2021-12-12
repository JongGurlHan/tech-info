## AOP란?

Spring의 핵심 개념중 하나인 DI가 애플리케이션 모듈들 간의 결합도를 낮춰준다면,   
AOP는 애플리케이션 전체에 걸쳐 사용되는 기능을 재사용하도록 지원하는 것이다.

AOP는 흩어진 Aspect들을 모아서 모듈화 하는 기법이다.
서로 다른 클래스라고 하더라도 비슷한 기능을 하는 부분(ex 비슷한 메서드, 비슷한 코드)이있다.  
이 부분을 Concern이라고 한다.(아래 색칠 되어 있는 부분)

<img width="546" alt="AOP" src="https://user-images.githubusercontent.com/60098769/145713936-d242543f-1fce-49df-afad-e2cf8aeb0a4a.png">

이 때 만약 노란색 기능을 수정하여야하면, 각각 클래스의 노란색 기능을 수정해주어야 하기 때문에, 유지 보수 면에서 불리하다.  

이것을 해결한 방법이 AOP이다.  

흩어진 기능들을 모을 때 사용하는 것이 Aspect이다.   
각각 Concern 별로 Aspect를 만들어주고, 어느 클래스에서 사용하는 지 입력해주는 방식이다.   
아래의 그림이 Aspect로 모듈화 한 것을 보여주는 것이다.

<img width="629" alt="AOP2" src="https://user-images.githubusercontent.com/60098769/145713974-8c020d8a-0f2e-4ebd-bb76-adcf34be188d.png">

각 모듈에는 Advice와 Pointcut이 들어있다.  

Advice란 해야할 일, 기능을 나타내는 것이다.  
Pointcut이란 어디에 적용해야하는지를 나타내는 것이다.(ex A라는 클래스의 W라는 메서드)  

Target이라는 개념도 있는데, Target이란 각각 클래스를 나타내는 것이다.(클래스 A, B, C) 즉, 적용이되는 대상을 뜻하는 용어이다.  

Join point라는 용어는 끼어들 지점을 뜻한다.(ex 메서드를 실행할 때, 필드에서 값을 가져갈 때 등등)  
