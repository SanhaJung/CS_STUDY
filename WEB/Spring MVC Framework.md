
# Spring MVC Framework

### 1.  MVC란?
> 디자인 페턴중 하나  
> model, view, controller의 요소로 나누어진 패턴  
> mvc1, mvc2로 구분됨
* **Model, View, Controller**
    * Model: 어플리케이션의 정보, 데이터, db등을 뜻함
    * View: 사용자에게 보여지는 화면. 즉, UI (Model로 부터 정보를 얻고 표시)
    * Controller: 데이터와 비즈니스 로직 사이의 상호작용 관리 (Model과 View 통제)
* **mvc1**
  <img src="https://i.imgur.com/rzhzcZc.png" >
  * JSP로 구현한 기존 웹 어플리케이션 모델 구조
  * JSP 페이지에 비즈니스 로직을 처리하기 위한 코드(Controller) 웹브라우저에 결과를 보여주기 위한 출력 관리 코드(view) 섞여있음.
  * JSP 페이지에서 표현(view), 저장(model), 처리(control)되므로 **재사용이 힘들고 가독성이 떨어짐**.  


    😎 정의: 모든 클라이언트 요청과 응답을 JSP가 담당하는 구조
    🙂 장점: 단순한 페이지 작성으로 쉽게 구현 가능, 중소형 프로젝트에 적합
    😡 단점: 웹 애플리케이션이 복잡해지면 유지보수 문제가 발생

* **mvc2**
  <img src="https://i.imgur.com/keastvz.png" >
  * Controller 역할을 Servlet이 함.
  * Servlet은 웹 브라우저 요청을 처리한 후 결과를 JSP 페이지로 포워딩.


    😎 정의: 클라이언트의 요청처리, 응답처리, 비즈니스 로직 처리 부분을 모듈화시킨 구조
    🙂 장점: controller분리로 유지보수와 확장 용이
    😡 단점: 설계를 위한 시간이 많이 소요되어 개발기간 증가

### 2. 스프링  MVC 프레임워크
<img src="https://i.imgur.com/blr7x6q.png" >  

| 구성요소                 | 내용                                                         |
|----------------------|------------------------------------------------------------|
| DispatcherServlet    | 클라이언트의 요청을 전달받아 요청에 맞는 컨트롤러가 리턴한 결과값을 View에 전달하여 알맞은 응답을 생성 |
| HandlerMapping       | 클라이언트의 요청 URL을 어떤 컨트롤러가 처리할지 결정                            |
| Controller           | 클라이언트의 요청을 처리한 뒤, 결과를 DispatcherServlet에게 리턴               |
| ModelAndView         | 컨트롤러가 처리한 결과 정보 및 뷰 선택에 필요한 정보를 담음                         |
| ViewResolver         | 컨트롤러의 처리 결과를 생성할 뷰를 결정                                     |
| View                 | 컨트롤러의 처리 결과 화면을 생성, JSP 또는 Velocity 템플릿 파일 등을 뷰로 사용        |

----
### 예상질문
📌스프링과 MVC 패턴에 대해 설명하세요.
> 스프링  
> 자바플렛폼을 위한 오픈소스 애플리케이션 프레임워크  
> 자바 ES로 된 자바 객체 POJO를 자바 EE에 의존적이지 않게 연결해주는 역할  
> 스프링의 특징은 크기, 부하 측면에서 경량시킨 것과, IOC 기술로 애플플리케이션의 느슨한 결합을 도모 시킴  
> MVC 패턴  
> 코드 재사용에 유용  
> 사용자 인터페이스, 응용 프로그램 개발에 소요되는 시간을 줄여주는 효과적인 설계 방식
> 구성요소는 MOdel, View, Controller  
> 모델은 핵심적이 비즈니스 로직 담당하여 db관리  
> 뷰는 사용자에게 보여주는 화면  
> 컨트롤러는 모델과 뷰 사이에서 정보교환할 수 있도록 연결

----
### 🔗Reference
* https://kim6394.tistory.com/161
* https://chanhuiseok.github.io/posts/spring-3/