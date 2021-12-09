# OAuth는 Open Authorization의 약어로 인증을 위한 오픈 스탠다드 프로토콜이다.

# 배경

사용자가 여러 어플리케이션에 자신의 비밀번호를 제공하고 싶지 않은 요구에서 시작 됨

또한 클라이언트도 개인정보 관리 책임을 서드파티 애플리케이션(google, kakao 등)에 위임할수 있다.

# keyWord

client - 서버

Resource Owner - 유저

Resource Server (ex, google, naver, kakao 등)

Authorization server - 인증/인가를 수행하는 서버로 클라이언트의 접근 자격을 확인하고 Access Token을 발급하여 권한을 부여하는 역할

# 대략적 동작 시퀀스

1.  인증이 필요한 서비스 -> 서버가 사용자에게 인증 페이지 제공(간편 로그인 api)
2.  클라이언트는 Authorization Server로 부터 검증 후 Token(Access token과 refresh token)과 정보를 제공받음
    접근을 위한 토큰 : access token
    access token을 발급받기 위한 토큰 : refresh token
    -----여기 까지 로그인
3.  클라이언트는 access token을 사용하여 Resource Server로 부터 자원 요청(서드파티 어플리케이션의 정보들)
4.  Resource Server는 Access token이 유효한지 확인 후 client에게 자원을 보냄
    만일, access token이 만료 되었거나 위조되었다면 refresh token을 통해 access token을 재발급 받음
    만일, refresh token도 만료 되었을 경우 1번으로 돌아가 서버가 유저에게 다시 인증을 요청함(재 로그인)
