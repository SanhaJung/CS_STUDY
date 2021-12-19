# [Spring Boot] SpringApplication

> 어플리케이션 실행 방법이다.

❗️ 방법1을 사용하면 SpringApplication이 제공하는 다양한 기능을 사용하기 어렵다.  
💡 SpringApplication 인스턴스를 생성하여 실행해서 커스터마이징하여 사용하자.

1. 간단한 방법

   ```java
   @SpringBootApplication
   public class SpringinitApplication {
   public static void main(String[] args) {
       SpringApplication.run(SpringinitApplication.class, args);
   }
   }
   ```

2. 커스터마이징 가능한 방법

   ```java
   @SpringBootApplication
   public class SpringinitApplication {
   public static void main(String[] args) {
       SpringApplication app = new SpringApplication(SpringinitApplication.class);
       app.run(args);
   }
   }
   ```

- @SpringBootApplication : 어노테이션을 통해 스프링 Bean을 읽어와서 자동으로 생성한다.
- 위 어노테이션이 있는 파일 위치부터 설정들을 읽어가기 때문에, <b>_프로젝트의 최상단_</b>에 만들어야 한다.
  <br/>
  <br/>

## 제공 기능

1.  Application 타입 지정

    - SERVLET : Spring MVC가 있다면 기본 타입
    - REACTIVE : Spring WebFlux가 있다면 기본 타입
    - NONE : 둘 다 없는 경우

    SERVLET -> REACTIVE -> NONE 순서로 작동한다.

    _WebFlux : Spring Framwork5에서 새롭게 추가된 모듈로, client-server에서 reactive 스타일의 어플리케이션 개발을 도와주는 모듈_

    <br>

2.  Log Level 설정  
     : 기본 로그레벨은 INFO레벨

    > 디버거 모드 : VM options에 _-Ddebug_ 또는 Program arguments에 _--debug_ 적어주기  
    > ❗️ 둘 중 하나만 적어야 한다.

<br>

3.  FailureAnalyzer

    > 어플리케이션 에러 발생 시 보기 쉽게 출력해주는 기능이다.

<br>

4.  Banner

    > src - main - resources에 Banner.txt를 넣어서 변경하기.

    - Banner.txt

      ```txt
      ______     ______        ______     ______   __  __     _____     __  __
      /\  ___\   /\  ___\      /\  ___\   /\__  _\ /\ \/\ \   /\  __-.  /\ \_\ \
      \ \ \____  \ \___  \     \ \___  \  \/_/\ \/ \ \ \_\ \  \ \ \/\ \ \ \____ \
      \ \_____\  \/\_____\     \/\_____\    \ \_\  \ \_____\  \ \____-  \/\_____\
      \/_____/   \/_____/      \/_____/     \/_/   \/_____/   \/____/   \/_____/
      ```

    - 실행 모습

      <img width="700" alt="Banner" src="https://user-images.githubusercontent.com/63037344/146664812-a530e511-fea6-4864-bf20-7d21c6b2f960.png">

<br>

5.  Application Event > Spring Boot에서 제공하는 다양한 시점의 이벤트들이다.

    ```java
    @Component
        public class DsunniListner implements ApplicationListener<ApplicationStartingEvent> {
            @Override
            public void onApplicationEvent(ApplicationStartingEvent applicationStartingEvent) {
            System.out.println("---------------------------");
            System.out.println(" Application is Starting ");
            System.out.println("---------------------------");
            }
        }

    ```

<hr/>

## 🔗 Reference

Banner 문자열 재밌게 바꾸기

- http://patorjk.com/software/taag/#p=display&f=Sub-Zero&t=CS%20Study

- https://velog.io/@dsunni/Spring-Boot-%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8-%ED%99%9C%EC%9A%A9-%EA%B8%B0%EB%8A%A5-%EC%86%8C%EA%B0%9C-Spring-Application
