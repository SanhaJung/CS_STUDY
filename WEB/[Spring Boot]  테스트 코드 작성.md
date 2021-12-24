# Spring Boot 테스트 코드 작성

## 1. TDD

> 테스트 주도 개발로 레드 그린 사이클을 따른다.

### 레드 그린 사이클

<img src="https://xengom.com/assets/images/2/TDD.png">

1. RED: 항상 실패하는 테스트를 먼저 작성
2. GREEN: 테스트가 통과하는 프로젝션 코드 작성
3. REFACTOR: 테스트가 통과하면 프로덕션 코드를 리팩토링

--> 우선 테스트를 작성하고 그걸 통과하는 코드를 만들고 해당 과정을 반복하여 제대로 동작하는지에대한 피드백을 받아들인다.

### TDD를 사용하는 이유

**적용전의 오류 수정 방식**

``` 
1. 서버 실행
2. 오류 발견
3. 서버 종료
4. 오류와 관련된 부분에 console.log를 사용하여 오류 탐색
5. 오류 수정 후 서버 실행
6. 오류가 수정되지 않았다면, 3-5를 반복
7. 오류 수정 완료
```

**적용 후 장점**

* 개발 단계 초기에 문제를 발견하게 해줌
* 추후 코드 리팩토링하거나 라이브러리 업그레이드등에서 기존기능이 올바르게 작동하는지 확인 가능
* 기능에 대한 불확실성을 감소시킴
* 시스템에 대한 실제 문서를 제공함. 즉, 단위 테스트 자체를 문서로 사용가능

### 단위 테스트

> 하나의 모듈을 기준으로 독립적을 ㅗ진행되는 가장 작은 단위의 테스트
>
> 하나의 기능 or 메소드

## 2.  테스트 코드 예제

#### 테스트 코드 예제

```
import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.WebMvcTest;
import org.springframework.test.context.junit4.SpringRunner;
import org.springframework.test.web.servlet.MockMvc;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.*;
import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.*;

@RunWith(SpringRunner.class)
@WebMvcTest(controllers = HomeController.class)
public class HomeControllerTest {

    @Autowired
    private MockMvc mvc;

    @Test
    public void home_return() throws Exception {
        //when
        String home = "home";

        //then
        mvc.perform(get("/home"))
                .andExpect(status().isOk())
                .andExpect(content().string(home));
    }
}
```



1. `@RunWith(SpringRunner.class)`
   * 테스트를 진행할 때 JUnit에 내장된 실행자 외에 다른 실행자(SpringRunner라는 스프링 실행자)를 실행
   * 스프링 부트 테스트와 JUnit 사이의 연결자 역할

2. `@WebMvcTest`
   * Web(Spring MVC)에 집중할 수 있는 어노테이션
   * @Controller, @ControllerAdvice 등 사용가능해짐
   * @Service, @Component, @Repository는 사용할 수 없다

3. `@Autowired`
   * 스프링이 관리하는 Bean을 주입

4. `MockMvc`

   * 웹 API를 테스트할 때 사용

   * HTTP GET, POST, DELETE 등에 대한 API 테스트가 가능

5. `mvc.perform(get("/home"))`
   * MockMvc를 통해 /home주소로 HTTP GET 요청
6. `status().isOk()`
   * HTTP Header의 Status 검증(200, 404, 500error같은 것)
   * 여기선 .isOk()이기 떄문에 200인지 아닌지 검증
7. `content().string(hello)`
   * 응답 본문의 내용 검증
   * otroller에서 hello를 리턴하기 때문에 이 값이 맞는지 검증

테스트에 통과하면 다음과 같이 `Tests passed`가 뜬다

프로젝트를 만들면서 다양한 기능들을 구현할때 코드로 견고한 프로젝트를 만들기 위한 기능별 단위 테스트를 진행하는 습관을 길러야 한다.

### 예상질문

📌 TDD를 적용하는 이유는 무엇인가요?

📌 프로젝트시 적용해 본 적이 있나요?

 # 🔗 Reference

https://xengom.com/springboot/springboot_testcode/

https://velog.io/@shelly/spring-boot-%EB%8B%A8%EC%9C%84-%ED%85%8C%EC%8A%A4%ED%8A%B8-%EC%BD%94%EB%93%9C-%EC%9E%91%EC%84%B1

https://velog.io/@swchoi0329/Spring-Boot-%ED%85%8C%EC%8A%A4%ED%8A%B8-%EC%BD%94%EB%93%9C-%EC%9E%91%EC%84%B1

https://velog.io/@shelly/spring-boot-%EB%8B%A8%EC%9C%84-%ED%85%8C%EC%8A%A4%ED%8A%B8-%EC%BD%94%EB%93%9C-%EC%9E%91%EC%84%B1