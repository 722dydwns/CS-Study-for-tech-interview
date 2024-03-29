[스터디 1주차 | HTTP](https://www.notion.so/1-HTTP-623151e5221c42429a2ab2be923fe965?pvs=21)

---

```java
HTTP
HTTPS(TLS,SSL)
HTTP 1.1 2.0 3.0
HTTP RESTFUL
HTTP 응답코드
```


→ 여기서 **HTTP**는 전송 계층 위에 있는 **애플리케이션 계층**(응용 프로그램이 사용되는 프로토콜 계층)이다.

# HTTP

**⬛ HTTP (HyperText Transfer Protocol)**

- 인터넷 상에서 클라이언트와 서버가 자원 주고 받을 때 쓰는 통신 규약
- 컴퓨터 간 데이터 통신 원활히 하기 위한 규약
- **서버-클라이언트 모델을 따라 데이터를 주고 받기 위한 프로토콜**
- HTTP는 **80번 포트** 사용하고 있다.

**2) HTTP 특징**

- **Stateless(무상태),  Connectionless (비연결성) 특징이 있다.**
- **따라서 요청에 대한 응답을 마치면 연결을 즉시 끊는다. (최소한의 자원으로 서버 유지할 수 있다.)**

**[장점] 서버 확장성 높다는 장점이 있다.**  매번 연결 끊고 상태유지를 하지 않기 때문에 다른 응답 서버로도 쉽게 바꿀 수 있다. 단순하다. 

**[단점] 매번 통신을 위한 연결을 새로 해야 하고, stateless 특징 때문에 쿠키나 세션 등의 공간에 상태를 저장할 공간이 별도로 필요하다.**

**3) HTTP의 비연결성, 무상태 특성을 보완하는 방법**

   **A. 쿠키, 세션을 통한 상태 기억** 

**A-1) 쿠키 (Cookie) : 클라이언트에 저장되는 key-value 데이터**

- 클라이언트 측에 데이터가 저장되기 때문에 보안에 취약
- 그래도 저장된 정보 바로 사용 가능해서 빠르다.

 **A-2) 세션 : 서버 측에서 관리하는 데이터**

- 세션 ID를 부여해 클라이언트를 구분하며 브라우저 종료 시 사라진다.
- 쿠키보다 보안에 안전하지만, 데이터 공간을 더 차지한다는 단점있다.
- 세션은 id를 통해 값을 가져와야 하므로 쿠기가 더 빠르다.

   **B. 웹 스토리지 (web Storage)** 

- 클라이언트에 데이터를 저장할 수 있도록 HTML5부터 추가된 저장소
- key-value 쌍의 데이터를 저장하는 게 쿠기와 비슷
- 쿠키는 매번 서버에 전송되지만, 스토리지는 클라이언트측에 저장만 될 뿐이다.

**B-1) 로컬 스토리지 (local Storage) | 영구적**

- 브라우저 종료해도 영구적 저장된다.
- 단, 동일 브라우저 사용 시에만 해당
- **지속적으로 필요한 데이터 저장** (ex 자동 로그인)

**B-2) 세션 스토리지 (session Storage) | 일시적**

- 브라우저 종료 시 사라진다.
- **일시적으로 필요한 데이터 저장** (일회성 로그인 정보, 입력폼 저장 )

   **C. 비연결성 보완을 위해 keep-alive 헤더 사용** 

- 기본적으로 HTTP는 비연결성(매번 연결 성립 후 데이터 주고받은 뒤 끊음)
- 그런데 HTTP/1.1 부터 keep alive 옵션을 제공하면서 지정된 시간동안 TCP 연결 끊지 않고 유지할 수 있어졌다.

**4) HTTP 구조** 

- HTTP 는 애플리케이션 레벨의 프로토콜로 TCP/IP 위에서 작동한다.
- HTTP는 상태를 갖지 않는 무상태 프로토콜이다.
- Method, Path, Version, Header, Body로 구성된다.


**5) HTTP 문제점** 

- HTTP는 텍스트 교환이므로 누군가 네트워크에서 신호 가로채면 내용이 노출되는 보안 이슈가 존재
- HTTP 는 **평문 데이터를 전송하는 프로토콜**이기 때문에 HTTP로 주요 정보를 주고받을 경우에는 제 3자에 의해 조회될 수 있는 문제점이 있다.
- **이러한 문제를 해결하기 위해 HTTP + 암호화 추가된 프로토콜 : HTTPS 가 등장한다.**

# HTTPS (TLS, SSL)

⬛ **HTTPS (Hyper Text Transfer Secure)**

- **HTTPS는 애플리케이션 계층과 전송계층 사이에 신뢰 계층인 SSL/TLS 계층을 넣은 ‘신뢰할 수 있는 HTTP 요청’ 을 의미한다.**
    
  
    
- 인터넷 상에서 **정보를 암호화하기 위해 (SSL or TLS 프로토콜) 위에 HTTP를 구현한 것**이다.
- 즉, 문서 전송시 **암호화 처리 유무에 따라** HTTP, HTTPS로 나누어진다.
- HTTPS는 **443번 포트 사용**한다.

**Q. 그럼 모든 사이트를 HTTPS 로 하는 게 좋을까 ?**

- → 암호화 과정으로 인한 속도 저하 발생하므로 필요한 경우에만 사용하라.

**⬛ HTTP와 HTTPS 의 차이점** 

**HTTP  : TCP - HTTP (직접 통신)**

**HTTPS  : TCP - SSL(TLS) - HTTP  (SSL/TLS를 경유한다)**

- 결국 가장 큰 차이는 SSL or TLS 이용 여부에 있다.
- HTTPS의 경우 SSL 또는 TLS 프로토콜 이용하여 데이터를 암호화해서 전송하기 때문에 제 3자가 감청하더라도 해독하기 어려워 기밀성이 유지된다.

**⬛ 암호화의 두 가지 유형 | SSL과 TLS**

- SSL/TLS를 사용하는 웸사이트 URL은 HTTP대신 HTTPS가 사용된다.

**1) SSL (Secure Socket Layer) : 암호화 기반 인터넷 보안 프로토콜**

- 클라이언트와 서버 간의 안전한 링크를 통해 송수신되는 모든 데이터를 안전하게 보장하는 ‘과거의’ 보안 표준 기술이다. → 현재는 TLS로 대체됨

**2) TLS (Tansport Layer Security)  : SSL의 업데이트 버전**

- 어플리케이션들이 네트워크 상에서 안전하게 통신하기 위해 사용된 프로토콜
- 서버와 클라이언트가 TLS로 통신할 떄, 어떠한 제 3자도 메시지를 변형시키거나 감청할 수 없도록 한다.
- 이 규약은 TCP/IP 네트워크를 사용하는 통신에 적용되며, 통신 과정에서 전송계층 종단 간 보안과 데이터 무결성을 확보해준다.

**⬛ 대칭키와 비대칭키**

1) **대칭키 암호화 방식 :** 암호화-복호화에 사용하는 키가 동일하다. ( 키 1개 사용됨)

- 암/복호화 속도가 1000배 정도 빠르다.
- 키 교환하는 와중에 탈취될 위험 있다. 연결하는 상대마다 키 생성해야 하므로 관리해야 할 키다 방대하게 많아진다.

//A키로 암호화하면 A키로 복호화 된다.

2) **비대칭키(공개키) 암호화 방식 :** 암호화-복호화에 사용하는 키가 서로 다르다 . (키 2개 사용됨)

- 느리다. 제한있다.
- 개인키로만 복호화 가능하기 때문에 기밀성을 제공한다.

//A키로 암호화하면 B키로 복호화가 된다.

<aside>
💡 예를 들어, A키와 B키가 있다고 해보자.

- 비대칭키의 경우, A키로 암호화하면 A키로 복호화하는 게 아니라 B키로 복호화할 수 있다.
- 반대로 B키로 암호화하면 A키로만 복호화할 수 있다.
- A,B키 중 하나는 개인키로 보관하고, 하나는 공개키로 보관하는데,
- 클라이언트가 공개키로 정보를 암호화해서 서버에 보내고, 서버는 갖고있던 개인키로 복호화한다.
- 결과적으로 공개키가 공개되어도, 누군가가 중간에 탈취해서 알 수 있는 정보들은 개인키로 암호화된 정보들 뿐이다.
</aside>

**⬛ 공개키, 개인키** 

- 공개키 : CA에 올려놓고 모두에게 공유
- 개인키 : 오직 서버만 가진

공개키로 암호화하고 보내면 복호화는 서버만 

⬛ **HTTPS 통신 과정 - SSL/TLS 핸드셰이크 과정 설명**

<aside>
💡 **암호화된 데이터를 전송하기 위해서 공개키(=비대칭키)와 대칭키를 혼합해서 사용**한다. 즉, 클라이언트와 서버가 주고받는 ‘실제 정보’는 대칭키 방식으로 암호화하고, 대칭키 방식으로 암호화된 실제 정보를 복호화할 때 사용할 대칭키’는 공개키 방식으로 암호화’해서 클라이언트와 서버가 주고 받는다.

</aside>

- **실제 데이터 : 대칭키 방식으로 암호화**
- **대칭키의 키 : 공개키(=비대칭키)**

//그럼 실제 데이터를 암호화한 대칭키를 서버-클라이언트 모두가 갖고 있어야 한다.

//그걸 공유할 때 활용하는 암호화 기법에는 비대칭키(공개키)를 활용한다.

- 사용자가 TLS를 사용하는 웹사이트를 접속하면 클라이언트와 웹 서버 간 TLS Handshake가 시작된다.
- 클라이언트는 서버의 인증서를 받아 서버의 무결성을 확인하고 신뢰할 수 있는 서버라면 암호화 통신에 사용할 대칭키를 서버의 공개키로 암호화하여 전달한다.
- 여기서 **데이터 주고받기 전 ‘서버의 무결성 확인하고 대칭키를 전달하는 과정’ 이 바로 SSL/TLS Handshake 이다.**
- **신뢰할 수 있는 사이트인지 일종의 탐색 과정을 거치게 되는데 이게 ‘TLS handshake’**
    
    ![img.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/f9e52833-0043-4562-9824-52c095ffd3df/img.png)
    

> **(1) clientHello : 클라이언트 안녕하세요 메시지**
> 
- 클라이언트가 서버에 tcp 연결을 위한 **‘client hello’ 메시지를 전송**한다.
- 이때 이 메시지에는 TLS 버전, 지원되는 암호화 제품군, 클라이언트 측에서 생성한 **랜덤 데이터를 서버에 보낸다.**

> **(2) serverHello : 서버 안녕하세요 메시지**
> 
- 서버가 클라이언트에게 ‘server hello’ 응답을 보내고 **해당 서버의 인증서와 함께 서버 측에서 생성한 랜덤 데이터를 클라이언트에 보낸다.**

//여기까지 (1)과 (2)로 서로 일단 악수 한 번 한 거임

//이제 클라이언트는 서버가 보내준 인증서가 ㄹㅇ 인지 CA를 통해 확인한다. (비대칭키, 공개키) 시스템을 사용해서 

// CA의 인증을 받은 인증서들은 해당 CA의 개인키로 암호화되어 있다.

//따라서,진짜 인증서라면 브라우저에 내장된 그 CA의 공개키로 복호화할 수 있다.

// 공개키로 복호화할 수 있는 인증서를 발급할 수 있는 건 그에 대응하는 개인키를 가진 CA 뿐이니까

> **(3) 인증 : 클라이언트는 서버가 보낸 인증서가 CA에서 발급된 것인지 확인한다.**
> 
- **클라이언트는 CA의 공개키를 이용해 SSL/TLS 인증서를 복호화하여 확인**한다.
- **서버가 정품인지, 클라이언트가 도메인 소유자와 통신하고 있는지 확인하기 위해 수행**한다.

> **(4) 예비 마스터 암호화**
> 
- **서버 랜덤 + 클라이언트 랜덤 데이터 조합 = pre master secret**
- 서버와 클라이언트의 랜덤 데이터를 이용해 pre master secret이라는 키를 만들고 공개키로 암호화해서 클라이언트가 서버에 보낸다.
- **클라이언트가** **pre master secret키를 공개키로 암호화하여 서버에 보내고**

> **(5) 개인 키 사용**
> 
- **서버에서는 개인키를 사용하여 premaster secret 키를 해독(복호화) 한다.**

//이로써 서버와 클라이언트는 모두 일련의 과정을 거쳐 pre master secret 값을 공유하게 된 거다.

// 서버와 클라이언트는 모두 일련의 과정을 거쳐서 pre master secret값을 master secret값으로 만든다.

- pre master secret 값을 **maser secret 값으로 만든다.**

> **(6) 세션 키 생성**
> 
- master secret 은 session key를 생성하는데, 이 세션 키 값을 이용해서 서버와 클라이언트는 대칭키 방식으로 암호화 한 후 주고 받는다.
- 이 master secret 값으로 세션 키(대칭키) 를 생성하는데 세션 키를 이용하여 이제 대칭키 방식의 통신을 한다.

//이로써 세션키를 클라이언트와 서버가 모두 공유하게 되었다. 

> **(7) 클라이언트 준비 완료**
> 

: 클라이언트가 세션 키로 암호화된 ‘완료’ 메시지를 보낸다.

> **(8) 서버 준비 완료**
> 

: 서버가 세션키로 암호화된 ‘완료’ 메시지를 보냅니다.

> **(9) 안전한 대칭 암호화 성공**
> 

: 핸드 쉐이크가 완료되고 세션키로 통신이 진행됩니다.

# HTTP(1.1 2.0 3.0)

**⬛ HTTP 버전별 특징 | 1.1  2.0   3.0** 

**1) HTTP / 1.0 버전**

- **기본적으로 한 연결 당 하나의 요청을 처리하도록 설계**되어 있다.
- 이는 **RTT를 증가**시킨다. (RTT : 패킷 왕복 시간)
- 서버로부터 파일 가져올 때마다 TCP 3-웨이 핸드셰이크를 게속해서 열어야 하기 때문
- 매번 연결 수립-끊기 하면 성능 떨어짐

**2) HTTP /1.1 버전 | 표준 프로토콜**

   (**1) Persistent Connection (keep-alive 기본 옵션으로 제공)**

- 연결 한 번 수립하면 데이터 교환 마칠 때까지 연결을 유지하고, 데이터 교환을 모두 끝내면 연결을 끊는 구조 (요청도 순서대로 처리)


   **(2) 파이프라이닝** 

- HTTP /1.0 은 매번 (요청→ 응답)순 으로 이루어져서 **한번에 연속된 요청이 왔을 경우 현재 처리 중인 요청에 대한 응답이 없다면 뒤이어 온 요청들이 무시되었다**.
- HTTP /1.1 부터는 하나의 Connection에서 응답 오기 전에도 여러 개의 순차적 요청을 보낼 수 있고, 응답도 그 순서에 맞춰 받는다.
- HTTP / 1.1에는 파이프라이닝이 추가되었다. **(하나의 Connections에서 요청에 대한 응답 오기 전에 순차적인 여러 요청을 보내고 보내고 그 순서에 맞춰 응답 받는 방식)**
- **동시 전송이 불가능**하고 한 번에 여러 개의 요청을 보낼 수 있지만, 그에 대한 응답은 여전히 순차적으로 이루어지기 때문에 요청 리소스 많아질수록 그에 비례하게 대기 시간도 길어진다.
- (순차적으로 처리하기 때문에 앞선 데이터 느리게 받아지면 뒤에 있는 것들은 대기하게 되어 다운로드 지연됨)
- 단점: 무거운 헤더 구조, HOLB 문제

<aside>
💡 HOLB 문제 : 패킷이 중간에 유실되거나 수신 측의 파싱 속도 느릴 때 통신에 병목 발생하게 되는 현상이다.

</aside>

**3) HTTP / 2.0 버전**

- 지연 시간 줄이고 응답시간 더 빠르게 하며 멀티플렉싱, 헤더 압축, 서버 푸시, 요청 우선순위 처리를 지원하는 프로토콜이다.
- HTTP 2.0 은 **하나의 Connection으로 ’동시에’ 여러 개의 메세지를 주고 받을 수 있다.**
- **즉, 요청 보낸 순서대로 응답 받지 않아도 되기 때문에 속도가 더 빠르다.**
- 여러 개의 연결 없이도 **병렬 처리 가능**해지며 **HOLB 문제**도 해결

**4) HTTP / 3.0 버전**

- HTTP 3.0 버전은  TCP가 아니라 **UDP를 기반으로 하는 QUIC 프로토콜**을 사용
- QUIC 프로토콜을 사용하기 때문에 새로운 연결에 대한TCP HandShake로 인한 지연 시간을 감소
- TCP 위에서 돌아가는 HTTP/2 와는 달리, QUIC 계층 위에서 돌아가며, UDP 기반으로 돌아가기 때문에 통신 시작 시 번거로운 3-way handshake 과정을 거치지 않아도 돼서 (초기 연결 설정 시 지연 시간 감소) 라는 장점이 있다.
- QUIC 프로토콜 : TCP가 가지는 문제점 해결하고자 구글이 개발한 UDP 기반 프로토콜

# HTTP RESTFUL

⬛ **HTTP RESTFUL**

- REST란 ? URL을 통해 자원을 명시하고, HTTP 메소드를 통해 자원을 처리하도록 설계된 아키텍쳐
- RESTful : REST 아키텍쳐를 구현하는 웹 서비스를 디자인한 것
- RESTful API : REST를 기반으로 서비스 API를 구현한 것

⬛ **REST에서 지원하는 HTTP 메서드**

1. GET -> 자원을 받아오기만 할 때 사용.
2. POST -> 새로운 자원을 추가할 때 사용.
3. PUT -> 존재하는 자원을 변경할 때 사용.
4. DELETE -> 자원을 삭제할 때 사용.
5. PATCH -> 데이터를 부분적으로 변경할 때 사용.


# HTTP 응답코드

**◼️ HTTP 상태코드 간략 설명**

1xx (Informational) : 요청이 수신되어 처리중 (거의 사용 X)

2xx (Successful) : 요청 정상 처리

3xx (Redirection) : 요청 완료하려면 추가행동 필요

4xx (Client Error) : 클라이언트 오류 때문에 서버가 요청 수행X

5xx (Server Error) : 서버 오류. 서버가 정상 요청 처리 X

**→ 만약 모르는 상태 코드가 나타나면, 상위 상태코드 번호로 해석하면 된다.**

**ex. 299 → 2xx (Successful)**

**ex. 451 → 4xx (Client Error)**

---

**200 상태코드 (Success)**

- 200 : OK. 클라이언트의 요청을 정상적으로 수행함
- 201 : Created. 클라이언트가 어떠한 리소스 생성을 요청, 해당 리소스가 성공적으로 생성됨 (POST를 통한 리소스 생성 작업 시, 또는 PUT)
- 202 : Accepted. 클라이언트의 요청은 정상적이나, 서버가 아직 요청을 완료하지 못함
- 204 : No Content. 클라이언트의 요청은 정상적이나 컨텐츠를 제공하지 않음

**300 상태코드** 

- 301 : 클라이언트가 요청한 리소스에 대한 URI가 변경되었을 때 사용하는 응답코드(응답 시 Location header에 변경된 URI를 적어줘야 함)

**400 상태코드 (클라이언트 오류)**

- 400 : Bad Request. 클라이언트의 요청이 부적절 할 경우 사용하는 응답 코드
- 401 : Unauthorized. 비인증. 클라이언트가 인증되지 않은 상태에서 보호된 리소스를 요청했을 때 사용하는 응답 코드
- 403 : Forbidden. 비인가. 유저의 인증상태와 관계없이 클라이언트가 권한이 없기 때문에 작업을 진행할 수 없는 경우
- 404 : Not Found. 클라이언트가 요청한 자원이 존재하지 않음
- 405 : Method Not Allowed. 클라이언트의 요청이 허용되지 않는 메소드(HTTP Method)인 경우. 즉, 자원(URI)는 존재하지만 해당 자원이 지원하지 않는 메소드일 때 응답하는 상태 코드.
- 409 : Conflict. 클라이언트의 요청이 서버의 상태와 충돌이 발생한 경우

**500 상태코드 (서버 오류)**

- 서버에 문제가 있을 경우 사용하는 응답 코드
- 5**00 Internal Server Error**

서버 내부 문제로 오류 발생.

애매하면 500 오류

- **503 Service Unavailable**

서비스 이용 불가

서버가 일시적 과부하 또는 예정된 작업으로 잠시 요청 처리할 수 없음

Retry-After 헤더 필드로 얼마뒤에 복구되는지 보낼 수도 있음

---