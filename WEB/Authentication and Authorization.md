
# Authentication(인증) vs Authorization(인가)

## 1. 인증
클라이언트가 자신이 주장하는 사용자와 같은 사용자인지 확인하는 과정( **로그인** )

## 2. 인가
권한부여 - 클라이언트가 하고자 하는 작업이 허가된 작업인지 확인( **권한** )


## 3. 인증과 인가의 차이점
**인증을거친 후** 인증된 사용자에게 사용자에 대한 **특정한 권한을 부여**한다.

## 4. 인증과 인가 적용
1. 인증(Authentication)
   1. 회원가입 과정
      1. id, pw 생성
      2. pw 암호화하여 DB에 저장
   2. 로그인 과정
      1. 등록된 id, pw 입력
      2. 암호화된 DB에 저장된 사용자의 비밀번호가 일치하는지 비교
      3. 일치한다면 로그인
      4. 로그인에 성공하면, Access Token을 클라이언트에 전송
      5. 최초 로그인 성공 후, 다음부터 Access Token을 첨부하여 서버에 요청을 전송하여 로그인과정 생략

2. 인가(Authorization)
   1. **인증**절차를 통해 access token 생성. 이 토큰에 사용자의 정보 포함(ex. user id)
   2. 사용자가 요청을 보낼때 access token을 첨부해서 보냄
   3. 서버에서 access token 복호화
   4. 복호화된 데이터를 통해 사용자 정보(ex. user id) 얻음
   5. 사용자 정보를 사용하여 DB에서 해당 유저의 권한(permission) 확인
   6. 유저가 충분한 권한을 가지고 있으면 해당 요청 처리
   7. 유저가 권한을 가지고 있지 않으면 Unauthorized Response(401) 혹은 다른 에러 코드 보냄

----
### 예상질문
📌인가 과정을 설명하세요.

📌인증과 인가의 차이점을 설명하세요.

----
### 🔗Reference
https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=taeyoun795&logNo=220588115319
https://velog.io/@aaronddy/%EC%9D%B8%EC%A6%9DAuthentication%EA%B3%BC-%EC%9D%B8%EA%B0%80Authorization
https://ivorycode.tistory.com/entry/%EC%9D%B8%EC%A6%9DAuthentication%EA%B3%BC-%EC%9D%B8%EA%B0%80Authorization