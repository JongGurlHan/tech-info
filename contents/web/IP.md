## ip

인터넷에서 특정 IP에서 특정IP로 정보를 전달할때 IP패킷이라는 통신단위로 메시지를 전달한다.   
IP패킷에는 내 IP, 목적지 IP, 메시지 등이 포함되어있다.

클라이언트 단에서 IP패킷정보를 인터넷 망에 던지면
목적지(200.200.200.2) 를 받을 수 있는 서버가 어디있는지 노드끼리 던지면서 찾고, 결국 서버에 도달한다.
![HTTP웹_기본지식_20201226_page-0015](https://user-images.githubusercontent.com/60098769/148686584-6b5e189e-5e79-4d21-af37-e0b5f4318e24.jpg)


 서버가 클라이언트로부터 정보를 받았다면 서버도 IP패킷을 만들어서  클라이언트로 던진다.  
 ![HTTP웹_기본지식_20201226_page-0016](https://user-images.githubusercontent.com/60098769/148686587-4ef68aa6-0b6f-4af6-b59f-ad5e71a7a89a.jpg)

<br><br>
### IP 프로토콜의 한계
- 비연결성
  -   패킷을 받을 대상이 없거나 서비스 불능 상태여도 패킷 전송
  ![HTTP웹_기본지식_20201226_page-0018](https://user-images.githubusercontent.com/60098769/148686934-e785da32-d104-4d15-87a7-1a71475520a6.jpg)
  
- 비 신뢰성
 
  - 중간에 패킷이 사라지면?
  ![HTTP웹_기본지식_20201226_page-0020](https://user-images.githubusercontent.com/60098769/148686936-548649e2-d7d8-4265-8c7d-9f48b0c11b12.jpg)
  - 패킷 전달 순서 문제 발생
  ![HTTP웹_기본지식_20201226_page-0021](https://user-images.githubusercontent.com/60098769/148686937-d1651251-529e-4743-b6d9-bf466af03716.jpg)
  
- 프로그램 구분
  - 같은 IP를 사용하는 서버에서 통신하는 애플리케이션이 둘 이상이면?

→ 이러한 문제를 해결하기 위해 나온게 **TCP 프로토콜**이다.
