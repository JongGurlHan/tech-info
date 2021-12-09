## Filter와 Interceptor 차이

### Filter, Interceptor
* 애플리케이션에서 자주 사용되는 기능(공통 부분)을 분리하여 관리할 수 있도록 스프링에서 제공하는 기능

![filterinterceptor](https://user-images.githubusercontent.com/60098769/145413963-89336663-5726-4047-8399-38b631b4484f.jpg)
1. 서버 실행 시 Servlet이 올라오는 동안 init 후 doFilter 실행
2. Dispatcher Servlet을 지나쳐 Interceptor의 preHandler 실행
3. 컨트롤러를 거쳐 내부 로직 수행 후, Interceptor의 postHandler 실행
4. doFilter 실행
5. Servlet 종료 시 destroy

#### Filter 특징
* Dispatcher Servlet 이전에 수행되고, 응답 처리에 대해서도 변경 및 조작 수행 가능
  * WAS 내의 ApplicationContext에서 등록된 필터가 실행
* WAS 구동 시 FilterMap이라는 배열에 등록되고, 실행 시 Filter chain을 구성하여 순차적으로 실행
* Spring Context 외부에 존재하여 Spring과 무관한 자원에 대해 동작
* 일반적으로 web.xml에 설정
* 예외 발생 시 Web Application에서 예외 처리
* ex. 인코딩 변환, XSS 방어 등
* 실행 메소드
  * init() : 필터 인스턴스 초기화
  * doFilter() : 실제 처리 로직
  * destroy() : 필터 인스턴스 종료

#### Interceptor 특징
* Dispatcher Servlet 이후 Controller 호출 전, 후에 끼어들어 기능 수행
* Spring Context 내부에서 Controller의 요청과 응답에 관여하며 모든 Bean에 접근 가능
* 일반적으로 servlet-context.xml에 설정
* 예외 발생 시 @ControllerAdvice에서 @ExceptionHandler를 사용해 예외 처리
* ex. 로그인 체크, 권한 체크, 로그 확인 등
* 실행 메소드
  * preHandler() : Controller 실행 전
  * postHandler() : Controller 실행 후
  * afterCompletion() : view Rendering 후

##### Filter, Interceptor 차이점 요약
* Filter는 WAS단에 설정되어 Spring과 무관한 자원에 대해 동작하고, Interceptor는 Spring Context 내부에 설정되어 컨트롤러 접근 전, 후에 가로채서 기능 동작
* Filter는 doFilter() 메소드만 있지만, Interceptor는 pre와 post로 명확하게 분리
* Interceptor의 경우 AOP 흉내 가능
  * handlerMethod(@RequestMapping을 사용해 매핑 된 @Controller의 메소드)를 파라미터로 제공하여 메소드 시그니처 등 추가 정보를 파악해 로직 실행 여부 판단 가능
