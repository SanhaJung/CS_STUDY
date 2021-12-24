# [Spring] Spring Security - 인증 및 권한 부여

> 스프링 기반의 애플리케이션의 보안(인증/권한/인가 등)을 담당하는 스프링 하위 프레임워크이다.

❗️ 권한 기능이 없는 API는 아무나 조회/수정/삭제가 가능하다는 문제점이 있다.  
💡 Spring Security를 사용하여 인증된 유저만 API를 사용할 수 있도록 한다.

<br>

## 보안 용어

- 접근 주체(Principal) : 보호된 리소스에 접근하는 대상

- 인증(Authentication) : 보호된 리소스에 접근한 대상에 대해 이 유저가 누구인지, 애플리케이션의 작업을 수행해도 되는 주체인지 확인하는 과정(ex. Form 기반 Login)

- 인가(Authorize) : 해당 리소스에 대해 접근 가능한 권한을 가지고 있는지 확인하는 과정(After Authentication, 인증 이후)

- 비밀번호(Credential) : Resource에 접근하는 대상의 비밀번호

- 권한 : 어떠한 리소스에 대한 접근 제한, 모든 리소스는 접근 제어 권한이 걸려있다. 즉, 인가 과정에서 해당 리소스에 대한 제한된 최소한의 권한을 가졌는지 확인.

<br>

## Spring Security Authentication Architecture

<details>
<summary>Form 로그인 상세 설명</summary>
<div markdown="1">

![spring-security-authentication-architecture](https://user-images.githubusercontent.com/63037344/147349089-b273bc28-594f-4f3b-bea4-f3242d3b997e.png)

1. 사용자가 form을 통해 로그인 정보를 입력 후, 인증 요청을 보낸다.

2. AuthenticationFilter가 HttpServletRequest에서 보낸 아이디와 패스워드를 인터셉트한다.

   - 안전을 위해 아이디와 패스워드의 유효성 검사를 실시한다.
   - 아이디와 패스워드를 인증용 객체(UsernamePasswordAuthenticationToken)로 만들어서 진짜 인증을 담당하는 AuthenticationManager인터페이스(구현체 - ProviderManager)에게 위임한다.

3. AuthenticationFilter에게 인증용 객체를 전달받는다.

4. 실제 인증을 할 AuthenticationProvider에게 인증용 객체를 다시 전달한다.
   _AuthenticationProvider : 스프링에서 인증을 담당하는 클래스_

5. DB에서 사용자 인증 정보를 가져올 UserDetailsService 객체에게 사용자 아이디를 넘겨주고 DB에서 인증에 사용할 사용자 정보(사용자 아이디, 암호화된 패스워드, 권한 등)를 UserDetails(인증용 객체와 도메인 객체를 분리하지 않기 위해서 실제 사용되는 도메인 객체에 UserDetails를 상속하기도 한다.)라는 객체로 전달 받는다.

6. AuthenticationProvider는 UserDetails 객체를 전달 받은 이후 실제 사용자의 입력정보와 UserDetails 객체를 가지고 인증을 시도한다.

7. 인증이 완료되면 사용자 정보를 가진 Authentication 객체를 SecurityContextHolder에 담은 이후 AuthenticationSuccessHandle를 실행한다.(실패시 AuthenticationFailureHandler를 실행한다.)

</div>
</details>

<br>
✓ API 인증 및 권한 부여를 위한 작업 순서

1. 회원 가입 / 로그인 API를 구현한다.
2. 리소스 접근 가능한 ROLE_USER 권한을 가입 회원에게 부여한다.
3. Spring Security 설정에서 ROLE_USER 권한을 가지면 접근 가능하도록 설정한다.
4. 권한이 있는 회원이 로그인 성공하면 리소스 접근 가능한 JWT 토큰을 발급한다.
5. 해당 회원은 권한이 필요한 API 접근 시 JWT 보안 토큰을 사용한다.

💡 접근 제한이 필요한 API에는 보안 토큰을 통해서 유저의 권한 여부를 Spring Security를 통해 확인하고, 리소스를 요청할 수 있도록 구성한다.

<br>

## Spring Security Filter

![spring-security-filter](https://user-images.githubusercontent.com/63037344/147349539-fb7da1d8-f353-4683-91e4-472f44d69a4f.png)

<hr/>

### 예상 질문

📌 Spring Security에 설명하고 사용하는 이유는 무엇인가요?

> 스프링 시큐리티는 스프링 기반의 애플리케이션의 보안(인증,권한 인가 등)을 담당하는 스프링 하위 프레임워크입니다. 보안과 관련해서 많은 옵션을 제공하기 때문에 개발자가 일일이 보안 관련 로직을 작성하지 않아도 된다는 장점이 있습니다.

<br/>

### 🔗 Reference

- https://www.bottlehs.com/springboot/%EC%8A%A4%ED%94%84%EB%A7%81-%EB%B6%80%ED%8A%B8-spring-security%EB%A5%BC-%ED%99%9C%EC%9A%A9%ED%95%9C-%EC%9D%B8%EC%A6%9D-%EB%B0%8F-%EA%B6%8C%ED%95%9C%EB%B6%80%EC%97%AC/

- Spring Security 로그인 구현 : https://kim-jong-hyun.tistory.com/33
