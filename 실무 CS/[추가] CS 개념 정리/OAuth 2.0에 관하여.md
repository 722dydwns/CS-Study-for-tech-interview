## OAuth 프로토콜이란 ?

OAuth = Open Authorization

- 인증을 위한 개방형 표준 프로토콜
- 클라이언트를 대신하여 리소스 서버에서 제공하는 자원에 대한 접근 궈한을 위임받는 방식
- 클라이언트가 사용자 인증 정보를 공유하지 않고도 자원에 접근할 수 있도록 하는 인증 방법

**→ 사용자 입장에서는 OAuth를 사용하면 민감 정보를 굳이 입력하지 않고도 신뢰할 수 있는 서버를 토대로 로그인 처리가 되고, 서버 입장에서도 민감 정보를 굳이 직접 관리하지 않아도 되는 이점이 있다.**

## **OAuth 1.0과 2.0 차이점**

OAuth 1.0과 OAuth 2.0 모두 API 봥ㄴ을 위한 프로토콜이다.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/2e914a55-2a1c-424f-b36e-db324a052485/Untitled.png)

### 1) 토큰 갱신

- OAuth 1.0 에서는 토큰 갱신이 어려웠다. (Access Token 유효기간 X)
- OAuth 2.0 에서는 새로운 토큰을 쉽게 발급받을 수 있다. (Access Token 유효기간 O)

→ 만약 유효기간 끝나면 Refresh Token으로 새 Access Token 발급 가능

### 2) 인증 방식

- OAuth 1.0 에서는 서명된 요청을 사용하여 사용자를 인증한다.
- OAuth 2.0 에서는 보안 토큰을 사용하여 인증한다.

### 3) 범용성

- OAuth 2.0는 보다 범용적인 프로토콜. (모바일 ~ 다양한 플랫폼에서 사용 O)
- OAuth 1.0은 덜 유연하며 웹에서 주로 사용

### 4) 승인 방식

- OAuth 1.0은 두 단계 승인 절차 사용
- OAuth 2.0은 보다 단순한 승인 절차 사용

## OAuth 2.0 이란 ?

- OAuth 2.0 방식은 리소스 서버에서 제공하는 사용자 신원에 대한 접근 권한을 서비스에 위임하는 방식 제공하는 것

## **OAuth 2.0 의 주체**

### **1) Resource Owner  (User)**

- 웹서비스 이용 유저

### **2) Client  (Application)**

- Resource Server 의 API를 사용하여 데이터를 가져오려고 하는 사이트
- Client는 Resource Owner를 대신하여 Authorization Server와 Resource Server에 접근하는 주체

### **3) Authorization Server  (권한 담당 서버)**

- Client가 Resource Server의 서비스를 사용할 수 있게 인증하고 토큰 발급해주는 서버

### **4) Resource Server (자원 담당 서버)**

- OAuth 2.0 서비스 제공하고 자원 관리하는 서버

## **OAuth 2.0 여러 인증 권한 과정**

### **中 Authorization Code Grant 방식 과정**

![166139288-61b86220-5cd8-4ee3-b577-4d437abdfa5c.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/2383f456-b001-4706-b1c8-1adb923e121d/166139288-61b86220-5cd8-4ee3-b577-4d437abdfa5c.png)

**1) User가 Client에 사용 요청을 보낸다.**

**2) Client는 권한 서버에 권한 부여 승인 코드를 요청한다.**

//이떄 요청에 포함되는 파라미터에는 response_type(code), client_id, redirect_uri, scope 매개변수로 보냄

**3) 클라이언트는 권한 서버에서 제공하는 로그인 페이지 (팝업)를 띄워 사용자에게 보여준다.**

**4) 사용자가 해당 로그인 페이지로 로그인을 하면, 권한 서버는 (권한 부여 승인 코드 요청 시 전달받았던) Redirect URL로 [권한 부여 승인 코드]를 전달한다.**

**5) Client는 다시 권한 서버로 [Authorization Code]를 전달하여 Access Token을 받는다.**

//로그인 성공 후 서비스 요청 및 리소스 제공 시 이 Access Token 사용함

//이제 Access Token 있기 떄문에 정해진 scope 영역 내에서 다양한 리소스 활용 가능하다.

**6) Client는 자신이 부여받은 Access Token을 DB에 저장하고,** 

**7) 이후 자원 요청 시 Access Token을 사용하여 Resource Server에 보호된 자원을 요청하고, 요청 자원을 전달받는다.**  

## **OAuth 2.0 Scope 이란?**

처음 로그인 요청 시 발급된 Access Token에는 scope을 정할 수 있고 Scope 정보를 가지고 있어 접근 범위를 제한하고 있다.

Client가 사용 가능한 Resource 접근 범위 영역 제한  

## **OAuth 2.0 보안 취약점**

- Redirection URI 조작 가능함
- 악의적 공격자가 인증 후 사용자를 클라이언트 대신 자신의 서버로 리다이렉트 할 수 있는 상황

## **OAuth 2.0 에서 사용되는 토큰 (2)**

### 1) Access Token

- 출입 접근용
- 유효시간 짧게 설정함

### 2) Refresh Token

- 만료 시 인증 연장용
- Access Token보다 유효시간 길게 설정하여, 만료 시 Refresh Token을 서버에 보내면 새 Access Token 발급받을 수 있음

[출처] https://blog.naver.com/seek316/222659353972