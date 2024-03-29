**웹 1 (OAuth, JWT, SSR 등)**

```
- OAuth & JWT & 인증 인가
- CSR vs SSR
- 서드 파티
```

---

## OAuth 2.0 관련 질문 모음

제 3의 서비스를 사용하기 위해 인증과 권한을 관리하는 프로토콜입니다. 

Oauth 2.0은 반드시 HTTPS를 사용해야 하고 Access Token의 만료기간이 무조건 존재합니다.

**→ Redirect URI는 기본적으로 보안을 위해 HTTPS만 허용된다.** 

### ✅ OAuth에 대해 간단히 설명해주세요.

OAuth는 제3자 인증 방식 입니다. 기본적으로 사용자는 서버를 신뢰할 수 없습니다. 그렇기 때문에, 민감정보를 작성하는 것을 꺼립니다. 서버측에서도 마찬가지 입니다. 사용자의 민감정보를 관리하는 것은 리소스가 필요합니다.

그래서 OAuth를 사용해서 신뢰할 수 있는 서버에게 정보를 맡겨놓고 접근할 수 있는 권한을 주는 것이라고 이해하면 됩니다. 그러면 사용자 측에서는 민감정보를 굳이 입력하지 않고도 서비스를 사용할 수 있고, 서버측에서도 민감정보를 굳이 관리하지 않아도 되기 때문에 이점이라고 볼 수 있습니다.

### ✅  OAuth 1.0과 2.0 차이를 설명해주세요.

1) OAuth 1.0 은 서명된 요청을 통해 보안을 유지하고, 2.0은 토큰 기반 접근을 사용하고 토큰을 통해 권한을 부여하여 보안을 유지한다.

2) OAuth 2.0 구현이 더 간단하며, 다양한 인증 방식 (인증코드, 암시적 인증, 패스워드 인증 등)을 지원한다.

**→ OAuth2.0이 더 간단하고 유연한 구조를 가지고 있으며 다양한 인증 및 인가 흐름을 지원한다.**

### ✅ OAuth 2.0를 사용하는 경우 어떤 장단점이 있나요.

> 장점
> 
1. 보안: 사용자는 자신의 아이디와 비밀번호를 직접 공유하지 않고, 제 3자 애플리케이션에 서비스 접근 권한을 부여할 수 있다. 이는 사용자의 인증 정보를 보호하며, 제 3자 애플리케이션에게 필요한 최소한의 권한만 부여하는데 도움이 된다.
2. 유연성: OAuth 2.0은 다양한 유형의 애플리케이션(웹, 모바일, 서버)을 지원하며, 다양한 시나리오에 맞게 설정할 수 있다.
3. 사용자 경험: 사용자는 한 번 로그인하여 다른 서비스에서 자신의 정보를 사용할 수 있도록 허용하면, 해당 서비스에 다시 로그인할 필요가 없어진다. 이는 사용자 경험을 향상시키며, 사용자가 여러 서비스를 쉽게 이용할 수 있도록 한다.

> 단점
> 
1. 복잡성: OAuth 2.0은 기술적으로 복잡한 프로토콜로, 구현이 어렵고 오류가 발생하기 쉽다. 따라서 적절한 보안 지침을 준수하고, 테스트와 유지 보수에 시간과 노력을 투자해야 한다.
2. 보안 취약점: 잘못 구현된 OAuth 2.0 시스템은 공격자가 인증 토큰을 가로채는 등의 보안 취약점을 가질 수 있다. 따라서 엄격한 보안 조치를 취해야 하며, 지속적인 보안 업데이트와 패치가 필요하다.
3. 중앙집중식: OAuth 2.0은 중앙 집중식 서비스에 의존적이다. 즉, 사용자가 신뢰하는 서비스(예: Google, Facebook 등)가 인증 과정을 처리한다. 이는 이러한 대형 서비스들이 사용자 데이터에 대한 엄청난 통제력을 가지게 되는 문제를 야기할 수 있다.

### ✅ OAuth2 를 사용한 사용자 인증 과정을 한번 순서대로 설명해보세요.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/459c2d4e-d9e2-4baa-bea5-0ab5f96f64cc/Untitled.png)

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

### ✅ OAuth 2.0에서 발생할 수 있는 보안 취약점 중 하나를 설명해주세요.

**리다이렉션 URI 조작**

이 취약점은 악의적 공격자가 인증 후 사용자를 클라이언트 대신 자신의 서버로 리다이렉트 할 수 있는 상황을 가리킵니다. 

이를 방지하기 위해서는 클라이언트 등록 시 리다이렉션 URI를 검증하고, 안전한 통신 및 인증 코드 교환을 보장해야 합니다.

공격자는 악의적인 URL을 주입하여 사용자를 피싱 사이트나 악성 웹 페이지로 리다이렉트시킬 수 있습니다.

OAuth와 같은 인증 및 권한 부여 프로토콜에서 리다이렉션 URI를 사용할 때 발생할 수 있습니다.

공격자가 리다이렉션 URI를 조작하여 허가받지 않은 액세스 토큰을 획득하거나, 피싱 공격을 수행할 수 있습니다.

### ✅ OAuth2.0에서 사용되는 토큰 종류 Access Token과 Refresh Token

Access Token : 만료시간이 있고 끝나면 다시 요청해야 한다.

Refresh Token : 만료되면 아예 처음부터 진행해야 한다.

---

## JWT 관련 질문 모음

### ✅ **JWT란 무엇인가?**

API 인증에 사용하는 토큰으로, Header와 Claim Set, Signature로 구성된 토큰입니다.

Header는 토큰을 어떻게 해석할지에 대한 정보를 담고 있으며, 토큰 복호화 시, 이 부분을 먼저 해석합니다. 이 부분은 암호화한 것이 아니라 `base64`로 변환한 것입니다.

Claim Set은 실제 데이터가 있는 부분으로 이 또한, 암호화한 것이 아니라 `base64`로 변환한 것입니다.

Signature는 앞서 말한 것돠 다르게 인코딩된 것이 아닌 `header인코딩값.claimSet인코딩값`을 암호화된 데이터입니다. 이 데이터를 통해 서버는 올바른 클라이언트에게 받은 토큰인지 인지할 수 있습니다.

### ✅ **JWT 장단점**

- 장점
    
    > JSON 형식으로 데이터를 저장해서 구조가 간단하다.
    > 
    > 
    > 토큰의 정보와 유효성 검증을 위한 서명이 포함되어 있어서, 서버 측에서 따로 토큰 상태를 저장할 필요가 없다.
    > 
    > 분산 시스템에서 잘 작동해, 여러 서비스 및 서버 간에 토큰을 교환하기 적합하다.
    > 
    > 인터넷 표준으로 정의되어 있고, 많은 프로그래밍 언어와 플랫폼에서 지원된다.
    > 
    > 서로 다른 도메인에서도 인증 및 권한 부여를 쉽게 수행할 수 있다.
    > 
- 단점
    
    > 토큰 자체에 정보를 저장하고 있기 때문에 보안에 주의해야 한다. 서버 측에서 안전하게 저장하고 관리해야 한다.
    > 
    > 
    > 토큰이 만료되기 전에는 변경이 어렵기 때문에 토큰을 취소하거나 갱신하는 메커니즘을 별도로 구현해야 한다.
    > 
    > 서명에 대한 보안을 제공하지만, 암호화는 제공하지 않아서 토큰 내용이 공격자에게 노출될 수 있다.
    > 
    > JWT의 서명을 검증하기 위해 키 관리가 필요하고, 이를 올바르게 관리해야 함
    > 

### ✅ JWT 토큰에 대해 설명해주세요.

**JWT는 JSON 포맷을 이용하는 Claim 기반의 웹 토큰이며, 토큰 자체를 정보로 사용하는 Self-Contained 방식으로 정보를 안전하게 전달합니다**

**.JWT는 헤더(Header).내용(Payload).서명(Signature)로 구성되며 각 파트를 점(.)으로 구분합니다.**

헤더(Header) : 토큰의 타입과 해시 암호화 알고리즘(방식지정)으로 이루어져 있다.

내용(Payload) : 토큰에 사용자가 담고자 하는 정보를 담는다. 내용에는 Claim이 담겨있고, JSON(Key/Value)형태의 한 쌍으로 이루어져 있다.

서명(Signature) : 토큰을 인코딩하거나 유효성 검증할 때 사용하는 고유한 암호화 코드이다. 헤더와 내용의 값을 인코딩한다.JWT(Json Web Token) 란 무엇일까? (서버 기반 인증 / 토큰 기반 인증)

### ✅ JWT 에 대해 간단히 설명해주세요.

JWT란 토큰 인증 방식에서 쓰이는 것이라고 볼 수 있습니다.

다른 사용으론 데이터를 공유하는데도 사용할 수 있지만 일반적으론 **토큰 인증 방식에서 사용**됩니다

**JWT는 헤더, 페이로드, 시그니쳐로 구분됩니다.**

- 헤더는 토큰의 타입, 암호화 알고리즘을 담고 있습니다.
- 페이로드는 토큰의 정보를 담고 있습니다. 등록된 클레임, 공개 클레임, 비공개 클레임들을 포함하고 있습니다.시그니처는 토큰의 정보가 신뢰할 수 있는 것인지 판단할 수 있도록 합니다.
- 시그니처는 헤더의 인코딩 값과, 정보의 인코딩 값을 합친 후 주어진 비밀키로 해쉬를 하여 생성합니다.

**JWT는 세션 기반 인증과 주로 대비됩니다.세션 기반 인증은 서버에서 세션 정보를 관리해야 하는 비용이 들게 됩니다.또한 분산 환경에서도 관리하기 어렵습니다.** 

**하지만 JWT는 그 자체로 정보를 가지고 있기 때문에 세션의 단점을 보완할 수 있습니다.**

### ✅ JWT에 사용자의 아이디와 비밀번호를 저장하려고 합니다. 문제가 있을까요

JWT는 사용자 id와 비밀번호를 저장하는데 사용해서는 안되는 방식입니다.

아이디와 비밀번호는 민감한 정보이며, 보안상의 이유로 안전하게 다뤄져야 합니다.

JWT는 주로 인증과 인가를 위한 토큰으로 사용되며, 아이디와 비번 같은 비밀정보를 저장하기에는 적합하지 않습니다.

**클라이언트 측에 저장된 정보는 잠재적으로 노출될 수 있고, JWT는 토큰 내에 데이터를 포함하는 구조라 아이디와 비밀번호를 저장하면 이러한 데이터가 토큰 내 노출될 수 있다.**

따라서, 아이디와 비밀번호는 안전한 방식으로 서버측에서 처리되어야 하고, 인증 후에는 사용자에게 토큰을 제공하여 클라이언트 측에서 권한 부여 및 세션 관리를 수행할 수 있다.

### ✅ RefreshToken을 설정할 때 당신이 고려해야 할 점은 ?

- 클라이언트 측에 노출되면 안되기 때문에 암호화하여 저장해야 한다.
- 수명을 적절히 관리해야 한다. 너무 긴 수명은 보안 위험이 있고, 너무 짧은 수명은 사용자 경험을 떨어뜨린다.
- 이 토큰을 클라이언트로 전송할 때 HTTPS를 사용하는 것이 좋다.

### ✅ 그렇다면 Bearer 인증 방식이 어떤것인가요? [?????]

**Bearer 타입 인증이란 Oauth2 에서 지원하는 토큰 기반 인증방식입니다.** 

Bearer과 Access토큰을 Authorization 헤더에 입력하는 인증방식입니다. 

Oauth2 인증방식에서는 SSL/TLS를 필수로 사용하기 때문에 Bearer 토큰을 쉽게 복호화할 수 없습니다.  또한 토큰에 유효기간을 부여하는 방식으로 안정성을 보장할 수 있습니다.

### ✅ **왜 JWT 방식을 사용해야 하는 건가 ? 세션과 비교해서**

JWT는 JSON Web Token의 약자로, 데이터가 JSON으로 이루어져 있는 토큰을 말한다. 

**[왜 사용했는지]**

기존의 세션인증방식은 인증 관련 정보를 세션 저장소라는 DB에 저장했기 때문에 서버가 과부하 되거나 서버를 확장하기 어려웠다. 

이를 보완하기 위해( = 서버자원을 절약) 사용자 인증에 필요한 정보를 토큰 자체에 담고 있어 별도 저장소에 정보를 저장해 둘 필요가 없는 JWT을 사용하게 되었다. 

토큰은 로그인 이후 서버가 만들어주는 문자열이고, 문자열 안에는 사용자의 로그인 정보와 서버의 서명이 들어있다. 사용자가 로그인을 하면 서버는 사용자에 토큰을 발급하고, 사용자는 토큰과 함께 다른 API 작업을 요청한다. 서버는 토큰의 유효성 검사를 통해 요청한 것에 대한 응답을 해준다. 단 한번 발급된 토큰은 수정 및 폐기가 불가하다는 단점이 있고, 유효기간을 짧게 지정해주는 것이 중요하다.

### ✅ JWT 이전에는 토큰 기반 인증 방식이 어떻게 진행되었나 ?

가장 유명한 타입이 Bearer 타입

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/c8ffd155-3a67-4c16-a422-bfbcae1911cf/Untitled.png)

### ✅ JWT와 OAuth의 차이

JWT는 토큰의 한 종류

OAuth는 토큰 발급하고 인증하는 Open 표준 프로토콜

**요약하자면, JWT는 클라이언트와 서버 간의 인증을 처리하기 위한 토큰이고, 토큰 자체에 정보를 포함합니다.** 

**반면, OAuth는 사용자의 인증과 권한 부여를 위한 프로토콜로, 클라이언트가 사용자의 동의를 얻어 제한된 액세스 토큰을 발급받아 자원에 접근합니다.**

**1) JWT (Json Web Token)**

- 클라이언트와 서버 간의 인증을 위한 토큰 기반 방식
- 일반적으로 웹 어플리케이션에서 사용되며, 클라이언트가 서버로 인증 정보 전달하면, 서버는 해당 정보 검증하여 사용자에 대한 인증 및 권한 부여를 수행한다.
- **JWT 토큰은 헤더,페이로드,서명으로 구성되어 있고 페이로드에는 사용자 정보 등 다양한 정보가 담고 있는 토큰이다.**

**2) OAuth (Open Authorization)**

- 사용자의 인증과 권한 부여를 위한 프로토콜
- 주로 사용자가 다른 웹 사이트나 애플리케이션에 로그인할 때 사용
- OAuth는 클라이언트 애플리케이션이 자원에 접근하기 위해 사용자의 동의를 얻고, 제한된 액세스 토큰을 발급받아 사용합니다. 보통 Bearer token을 발급
- **OAuth Token은 사용자의 중요한 정보는 담고 있지 않고 일종의 랜덤한 문자열.**

---

## 인증& 인가 관련 질문 모음

### ✅ 인증과 인가의 차이점 설명

- **인증은 Authentication**

 사용자가 서비스에 가입되어 있는지 확인하는 과정으로

 웹 서비스의 경우 아이디와 패스워드를 사용해 인증 과정을 수행합니다. 로그인 과정에서 주로 진행되며, 사용자가 서비스에 접근할 수 있는지 확인합니다.

- **인가는 Authorization**

 인증된 사용자에 대해 자원이나 작업에 대한 권한을 확인하는 과정으로

 로그인 과정에서 진행되는 인증과 달리 인가는 사용자가 request를 할 때마다 서버에서 권한을 확인합니다.

**✔️인증(Autentication):**

"넌 누구냐!"

-> 사용자가 누구인지 확인하는 것 (대표적인 예: 회원가입, 로그인)

**✔️인가(Authorization)**

: "너구나? 통과!"

-> 사용자의 요청에 대해 권한을 확인하는 것 (대표적인 예: "관리자"권한이 있는 사용자에게만 "관리자 페이지" 접근 권한 허락)

### ✅ 인증 Authentication 프로세스

**1-1. 로그인 요청:**

사용자(클라이언트)가 아이디와 비밀번호를 입력하고 로그인을 요청합니다.

**1-2. 사용자 확인:**

DB에 저장된 사용자의 비밀번호와 사용자가 입력한 비밀번호를 비교해보고, 인증 여부를 결정합니다.

**1-3. 토큰 발급:**

비밀번호가 일치하면, 사용자의 정보가 담긴 일종의 출입증인 "토큰"을 사용자에게 전송합니다.

*(아니, 뭘 어떻게 준다고요..? 이 프로세스 이해에 필수적인 토큰, 세션, 쿠키를 아래서 다시 설명합니다.)*

**1-4. 상태 유지:**

사용자는 이제 토큰을 받았으니, 이제 다음 요청부터는 ID, PW가 아닌 이 토큰을 제시하면 됩니다.

### ✅ 인가 Authorization 프로세스

- 인가를 위해서는, 인증이 선행되어야 합니다. 기억하세요, 선인증 후인가!

**2-1.  데이터 요청:** 

사용자는 관리자에게만 허용된 페이지로 넘어가려 합니다. 서버에 페이지 요청과 함께, 아까 발급받은 토큰도 쓱 내밉니다.

**2-2. 토큰 검증:**

서버는 토큰을 보고 어떤 사용자가 요청했는 지를 식별한 후, DB에서 사용자가 이 페이지에 접근할 권한이 있는 지 확인합니다.

**2-3. 인가 처리:**

사용자의 권한이 확인되면, 요청을 처리해줍니다.

---

## CSR & SSR 관련 질문 모음

### ✅ S**PA와 MPA란 ?**

**1) SPA (Single Page Application)**

- 한 개 Page로 구성된 애플리케이션
- 요청 시 최초 1번 필요한 모든 정적 리소스 다운로드함
- **그래서 SPA를 CSR 방식으로 렌더링한다고 말한다.**

**2) MPA (Multi Page Application)**

- 여러 개 Page로 구성된 애플리케이션
- 요청할 때마다 정적 리소스 다운로드되어 매번 전체 페이지 다시 렌더링됨
- **그래서 MPA를 SSR 방식으로 렌더링한다고 말한다.**

### ✅ SSR 의 정의

Server Side Rendering : 말 그대로 서버 쪽에서 렌더링 준비 마친 상태로 클라이언트에 전달하는 방식이다.

**SSR : 클라이언트에서 요청할 때마다 각 상황에 맞는 HTML 파일을 넘겨주기 때문에 페이지가 여러 가지일 수밖에 없습니다. 그러므로 MPA 구동 방식과 밀접한 관계가 있습니다.**

### ✅ CSR의 정의

Client Side Rendering : 말 그래도 클라이언트 쪽에서 렌더링이 일어난다.

**CSR : 최초에 한번 서버에서 전체 페이지를 로딩하여 보여주고 이후에는 사용자의 요청이 올 때마다, 리소스를 서버에서 제공한 후 클라이언트가 해석하고 렌더링하는 방식이다. SEO가 어렵다는 큰 단점이 있다.**

### ✅ CSR 과 SSR 차이점에 대해 설명해주세요.

렌더링 방식이란 결국 화면에 그려지는 것은 HTML이지만 이것을 누가 하느냐 주최에 따라서 CSR과 SSR로 나누어진다.

**CSR과 SSR의 차이점은 페이지가 렌더링되는 ‘위치’ 입니다.**

SSR(Server Side Rendering)은 서버에서 렌더링하고, SEO(Search Engine Optimization)와 웹 페이지 첫 화면 렌더링 속도가 빠릅니다.

CSR(Client Side Rendering)은 클라이언트에서 렌더링하고, SSR에 비해 월등한 사용자와 상호작용을 제공할 수 있습니다. 

따라서 요즘은 상황에 따라 SSR과 CSR을 합쳐 각 장점을 취하는 것이 트렌드 입니다.

### ✅ CSR과 SSR의 장단점에 대해서 답변해주세요.

**CSR (Client-Side Rendering):** 초기 페이지 로드는 느리지만 후속 페이지 로드가 빠르며, 인터넷 없이도 실행 가능하나 SEO에 불리함.

**SSR (Server-Side Rendering):** 초기 페이지 로딩이 빠르고 SEO에 우수하지만 페이지 이동 시 TTFB가 느리며 서버 호스팅이 필요하다.

- **CSR 과 SSR의 장단점 상세**
    
    ### **CSR (Client-Side Rendering)**
    
    **장점:**
    
    1. **후속 페이지 로드 시간 감소:** 이미 로드된 스크립트를 활용하여 빠른 후속 페이지 로딩.
    2. **인터넷 없이 실행 가능:** 캐싱된 스크립트로 인터넷 없이 어플리케이션 실행 가능.
    
    **단점:**
    
    1. **초기 페이지 로드 시간 느림:** 필요한 데이터를 받아오기 위해 초기에 모든 스크립트를 로드해야 함.
    2. **SEO에 불리함:** 검색엔진 최적화가 어려워 검색 결과에 제한적으로 노출될 수 있음.
    
    ### **SSR (Server-Side Rendering)**
    
    **장점:**
    
    1. **초기 페이지 로드 시간 빠름:** 렌더링이 준비된 파일을 서버에서 바로 로드하여 빠른 초기 로딩.
    2. **SEO에 우수:** 검색엔진이 콘텐츠를 수집하기 용이해 검색 결과에 잘 노출됨.
    
    **단점:**
    
    1. **페이지 이동 시 TTFB 느림:** 서버에서 페이지 생성 시간으로 인해 페이지 이동마다 TTFB가 느릴 수 있음.
    2. **서버 호스팅 필요:** 서버에서 렌더링을 실행하기 때문에 서버 호스팅이 필요.

### ✅ CSR 동작 방식 설명하시오.

1. 사용자가 웹 페이지를 방문하면 (request) 브라우저는 최소한의 HTML파일을 다운로드 (response)한다. 이 HTML 파일은 script, meta, link 등의 태그를 포함하며, 빈 컨텐츠의 index.html 파일이라고 보면 된다.
2. 브라우저는 index.html 파일에 있는 자바스크립트 번들 파일을 다운로드 한 다음, AJAX를 통해 API 요청을 수행하여 동적 컨텐츠를 가져오고 파싱하여 최종 컨텐츠를 렌더링한다.
3. 사용자가 페이지를 이동할 경우, 서버에 추가 HTML 파일을 요청하지 않고 이미 받은 자바 스크립트를 이용하여 렌더링한다.

### ✅ SSR 동작 방식 설명하시오.

1. 사용자가 웹 페이지를 방문하면(request), 서버는 리소스를 확인하고 페이지 내에 있는 서버측 스크립트를 실행 후 HTML 컨텐츠를 컴파일 및 준비한다.
2. 컴파일된 HTML은 추가 렌더링 및 표시를 위해 클라이언트 브라우저로 전송된다(response)
3. 브라우저는 HTML을 다운로드하고 최종 사용자가 사이트를 볼 수 있도록 한다.
4. 브라우저는 자바스크립트를 다운로드하고 실행하면서 페이지를 대화형(interactive)으로 만든다.
5. 사용자가 페이지를 이동할 경우**, 위 동작을 반복한다.**

### ✅ SSR 과 CSR을 각각 언제 사용하는 게 더 적합한가 ?

**SSR을 사용하자**

- 네트워크가 느릴 때 😓(CSR은 한번에 모든 것을 불러오지만 SSR은 각 페이지마다 나눠불러오기 때문)
- SEO(serach engine optimization : 검색 엔진 최적화)가 필요할 때.
- 최초 로딩이 빨라야하는 사이트를 개발 할 때
- 메인 스크립트가 크고 로딩이 매우 느릴 때CSR은 메인스크립트가 로딩이 끝나면 API로 데이터 요청을 보낸다. 하지만 SSR은 한번의 요청에 아예 렌더가 가능한 페이지가 돌아온다.
- 웹 사이트가 상호작용이 별로 없을 때.

**CSR을 사용하자**

- 네트워크가 빠를 때
- 서버의 성능이 좋지 않을 때
- 사용자에게 보여줘야 하는 데이터의 양이 많을 때.(로딩창을 띄울 수 있는 장점이 있다.)
- 메인 스크립트가 가벼울 때
- SEO 따윈 관심 없을 때😤
- 웹 어플리케이션에 사용자와 상호작용할 것들이 많을 때. (아예 렌더링 되지 않아서 사용자의 행동을 막는 것이 경험에 오히려 유리함.)

---

## Third Party 관련 질문 모음 써드파티

### ✅ **3rd party (Third Party) 란?**

하드웨어 생산자와 소프트웨어 개발자의 관계를 나타낼 때 사용한다.

그 중에서 **서드파티**는, 프로그래밍을 도와주는 라이브러리를 만드는 외부 생산자를 뜻한다.

### ✅**서드파티 (Thrid Party, 3rd party) 란?**

**1) 사전적 개념**

- 제조사와 소비자를 연결해주는 **회사 또는 제 3자를 칭하는 단어**이다.

ex) 게임제조사와 소비자를 연결해주는 게임회사(퍼블리싱)의 관계라고 볼 수 있다.

**2) 개발 서드파티**

프로그래밍의 서드파티는 개발을 하다보면, 편하고 효율적인 개발을 위해 플러그인 이나 라이브러리 또는 프레임워크 등을 사용한다.

ex) 프로그래밍 개발 과 개발자 사이의 서드파티는 플러그인, 라이브러리, 프레임워크가 될 수 있다.

**3) 그 외** 

최근에 Spring Boot 와 Redis 로 Cache 를 구현하는데 서드파티라는 단어가 나와서 이 글을 작성 하게 되었다.

Redis 는 **Spring Boot 와 Cache 사이의 Cahce 를 저장하는 서드파티(외부 프로그램)** 라고 볼 수 있다.

Redux는 아마 리액트에서 가장 널리 사용되는 서드파티 (third party) global state 라이브러리 일 것입니다. 

출처:

[https://socaeri.com/entry/프론트엔드-FE-기술면접-복기-모음](https://socaeri.com/entry/%ED%94%84%EB%A1%A0%ED%8A%B8%EC%97%94%EB%93%9C-FE-%EA%B8%B0%EC%88%A0%EB%A9%B4%EC%A0%91-%EB%B3%B5%EA%B8%B0-%EB%AA%A8%EC%9D%8C)

[밤토리:티스토리]

[https://github.com/NKLCWDT/cs/blob/main/Network/Cookie%2C Session%2C JWT.md](https://github.com/NKLCWDT/cs/blob/main/Network/Cookie%2C%20Session%2C%20JWT.md)

출처:

https://lisoft.tistory.com/22

[Benn의 삽질 저장소:티스토리]

출처:

https://dev-coco.tistory.com/164

[슬기로운 개발생활:티스토리]

[출처] [https://velog.io/@sheisalice606/기술면접-프로젝트1-예상-질문과-답변OAuth2-JWT-Bearer](https://velog.io/@sheisalice606/%EA%B8%B0%EC%88%A0%EB%A9%B4%EC%A0%91-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B81-%EC%98%88%EC%83%81-%EC%A7%88%EB%AC%B8%EA%B3%BC-%EB%8B%B5%EB%B3%80OAuth2-JWT-Bearer)
