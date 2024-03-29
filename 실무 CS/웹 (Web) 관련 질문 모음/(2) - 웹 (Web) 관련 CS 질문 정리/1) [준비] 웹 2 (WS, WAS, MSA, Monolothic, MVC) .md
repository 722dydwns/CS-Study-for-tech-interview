```
- 웹서버 vs WAS (with 서블릿)
- MSA vs Mnolithic
- MVC 패턴
```

---

## 웹서버 vs WAS (with 서블릿) 관련

### **✅ WS (Web Server) 에 대해 설명해주세요.**

ex Apache, Nginx

- HTTP 프로토콜 기반으로 클라이언트에게 정적 컨텐츠 제공하기 위한 서버
- 비즈니스 로직 넣을 수 X
- 사용자의 요청을 가장 먼저 받는다.

1) 정적 컨텐츠는 곧장 제공 (WAS 까지 거치지 않고 WS 선에서 바로 자원 제공)

2) 동적 컨텐츠 요청은 WAS에 넘기고 그 동적 컨텐츠 응답을 받아 클라이언트에게 전달

### **✅ WAS (Web Application Server)에 대해 설명해주세요.**

ex Tomcat

- DB 조회 혹은 다양한 로직 처리를 요구하는 동적 컨텐츠를 제공하기 위해 만들어진 Application 서버
- **비즈니스 로직 O 로직에 맞게 자원을 생성**
- WAS = Web Server + Web Container

### **✅ WS는 왜 필요한가요 ?**

- 웹 서버를 통해 정적 컨텐츠들은 Application Server까지 가지 않고, 앞단에서 빠르게 보내진다.
- 즉, 정적 컨텐츠만 처리 가능하도록 기능 분배하여 서버 부담 줄인다.
- 미리 만들어놓는 건가 ?

### **✅ WAS는 왜 필요한가요 ?**

- 웹 페이지에는 정적, 동적 컨텐츠가 모두 존재한다.
- WS 만 사용하면 원하는 요청에 대한 결과값을 모두 만들어놓아야한다. ???
- 그러면 자원 부족해지는 문제 발생한다.
- 따라서 WAS 를 통해 요청에 맞는 데이터를 DB에서 가져와 비즈니스 로직에 맞춰서 그때 그때 결과를 만들어 제공함으로써 자원을 효율적으로 사용할 수 있게 된다.

### **✅ WAS 가 WS 의 기능을 모두 수행하면 안되나 ? ( WS는 필요 없는 것인가)**

### **✅ WS와 WAS 즉, (Web Server와 Web Application Server) 차이점 설명하시오.**

가장 큰 차이점은 **‘동적 컨텐츠를 다룰 수 있는가’** 입니다.

**1) 웹 서버는 처리할 수 있는 데이터가 ‘정적 컨텐츠’ (html, css, 이미지) 로 한정됩니다.**

**2) 반면, 웹 어플리케이션 서버에서는 정적 + 동적 컨텐츠까지도 처리할 수 있습니다.**

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e2aaace0-24ef-4ae8-bed4-d8cb2e34acd9/184ea39b-4de2-4205-9648-83d3a7c5a797/Untitled.png)

→ 그 이유는 웹 어플리케이션 서버가 웹 서버에 웹 컨테이너를 붙인 형태이기 때문입니다. 그래서 정적 컨텐츠에 대해서는 WS에서 철하여 응답하고, 동적 컨텐츠일 경우 Web Container로 보내서 동적 컨텐츠에 대한 응답을 해줍니다.

### **✅ Apache(웹 서버 일종)는 멀티 프로세스인가, 멀티 스레드인가 ?**

아파치는 기본적으로 멀티 프로세스로 구현되어 있다. 하지만 설정에 따라 멀티 스레드를 같이 운용할 수 있다.

### **✅ Tomcat (WAS 일종)는 멀티 프로세스인가, 멀티 스레드인가?**

톰캣은 요청 처리하기 위한 **스레드 풀을 관리하고 있다.**

그리고 요청이 들어오면 해당 스레드 풀에서 스레드를 꺼내 요청을 처리하도록 한다.

## MSA vs Mnotithic 관련

1. 모놀리식 아키텍처와 MSA에 대해 아시나요?
2. 두개의 차이는 무엇인가요?
3. 어떤 장점과 단점이 존재하나요?

### **✅ Monolithic Architecture 에 대하여 설명해주세요.**

- **애플리케이션 구성 요소가 1개로 되어있는 형태**
- **모든 시스템의 구성요소가 한 프로젝트에 통합되어 있는 형태**

### **✅ Monolithic Architecture의 장단점을 설명해주세요.**

**장점**

- End-to-End 테스트 용이 (즉, 끝에서 끝까지 애플리케이션 시작~끝까지의 테스트 비용이 적다
- 개발 초기에는 단순한 구조 때문에 개발 용이하다는 게 장점

**단점**

- 작은 수정사항에도 전체를 빌드/배포해야 되는 문제
- 한 개의 에러가 전체 서버를 죽이는 문제
- 규모가 커질수록 복잡성 증

### **✅ MSA (MicrosService Architecture) 에 대하여 설명해주세요.**

- Monolithic Architecture의 한계점을 극복하고자 등장
- 애플리케이션 내의 다양한 서비스를 구성 요소화 시켰다.
- MSA는 1개의 시스템을 독립적으로 배포 가능한 각각의 서비스로 분할한다.
- 각각의 서비스느 RESTful API를 통해 데이터를 주고받으며 1개의 큰 서비스를 구성한다.
- 즉, 각 서비스가 독립적이기 때문에 업데이트 용이

### **✅ MSA (MicrosService Architecture)의 장단점을 설명해주세요.**

**장점** 

- 각 도메인 별 서비스 배포 운용 하므로 (결합도 낮아짐)
- 배포가 유연함
- 일부 서비스에 장애 발생해도 전체 서비스에 장애 발생 X
- 각 서비스들은 서로 다른 언어와 프레임워크로 구성 가능
- 재사용성 및 확장성 좋다.

**단점** 

- 서비스가 분리되어 있어, 테스팅이나 트랜잭션 처리가 어렵다.
- 서비스 간 RESTful API로 통신하기 때문에 그에 대한 비용 발생
- 서비스 간 호출이 연속적이라 디버깅 어렵다.

### **✅** 모놀리식 아키텍처 특징

- **Simplicity (심플함) :** 한 개의 서비스로 운용하기 때문에 구조는 심플
- **Consistency (일관성) :** 한 개의 서비스에서 프로세스가 돌아가기 때문에 일관성 유지 가능

     cf.  MSA의 경우 다양한 서비스를 통하기 떄문에 일관성 유지 어려울 수 있다.

- **Inter-module refactoring (모듈 간 리팩토링) :** 한 개의 서비스에서 통신 오가기 때문에 모듈 간 리팩토링 용이

      cf. MSA의 경우 각기 다른 서비스에서의 통신 있기 때문에 상당히 어려운 편

### **✅** 마이크로서비스 아키텍처 특징

- **Partial Deployment (부분 배포) :** 서비스가 부품화되어 있어 업데이트 용이
- **Availability (가용성) :** 자동배포 바탕이 되므로 하루에 새로운 배포 이루어지더라도 서비스는 끊임없이 제공된다.
- **Preserve Modularity (모듈성 유지) :** 서비스들이 분리되어 있어서 상호모듈 간 영향 X 깨끗한 종속성 갖는다.
- **Muliple Platforms (다중 플랫폼, 언어) :** 서비스 분리되어 있어서 상황에 맞게 여러 프로그래밍 언어 사용 가능

---

## MVC 패턴 관련

### **✅ MVC 패턴이란 ?**

Model-View-Controller 구조로 아키텍처 설계하기 위한 디자인 패턴이다.

- Model : 비즈니스 로직 처리 (Service, DAO 등)
- View : 사용자 UI
- Controller : Model과 View 사이 잇, 경로별 매핑하는 역할

### **✅ Spring MVC 란 ?**

웹 어플리케이션 개발을 위한 MVC 디자인 패턴 기반의 웹 프레임워크이다.

역시 구성요소는 Model, View, Controller 구조이다.

### **✅ Spring MVC 구성 컴포턴트**

- Dispatcher Servlet : 클라이언트 요청 가장 먼저 받아들이는 서블릿(요청에 맞는 컨트롤러에게 요청 전달)
- Handler Mapping : 해당 요청이 어떤 컨트롤러에게 온 요청인지 검사
- Controller: 클라이언트 요청에 대한 처리 결과는 Dispatcher Servlet에 전달
- ViewResolver : View 이름 통해 알맞은 View 찾음
- View : 사용자에게 보여줄 UI

### **✅ Spring MVC 작동 원리**

1) 클라이언트는 URL을 통해 요청 전송

2) 디스패처 서블릿은 핸들러 매핑을 통해 해당 요청이 어느 컨트롤러에게 온 요청인지 찾는다.

3) 디스패처 서블릿은 핸들러 어댑터에게 요청의 전달 맡긴다.

4) 핸들러 어댑터는 해당 컨트롤러에 요청 전달한다.

5) 컨트롤러는 처리 결과를 반환할 뷰 이름 반환한다.

6) 디스패처 서블릿은 View Resolver를 통해 반환할 뷰 찾는다.

7) 디스패처 서블릿은 컨트롤러에서 뷰에 전달할 데이터를 추가한다.

8) 데이터가 추가된 뷰를 반환한다.

### **✅ MVC 패턴 등장 이유 설명해주세요.**

세 구성요소로 독립적으로 개발하는 것이 ‘생산성’ 좋기 때문이다.

1) 구성요소들의 재사용 가능

2) 확장성 증가

3) 중복 코드 줄어듬

4) 각 요소에 집중하며 개발 가능

### **✅ MVC 패턴의 모델1과 모델2 차이점을 설명해주세요.**

**1) MVC 모델 1 : 뷰와 컨트롤러의 역할이 합쳐짐** 

- JSP가 View와 Controller를 모두 JSP가 담당하는 형태
- 사용자의 요청을 JSP가 받고 Java Bean 호출하여 처리하고 반환

**2) MVC 모델 2 : 뷰와 컨트롤러 역할이 분리됨**

- JSP 와 Servlet 모두 사용하여, View와 Controller를 분리한다.
- 웹 브라우저의 요청은 컨트롤러가 받고, 모델에서 요청에 대한 결과를 도출한 뒤 컨트롤러가 뷰 선택하여 데이터 전달하면 뷰는 오직 화면 출력만 한다.

**1) Model1 은 View와 Controller를 JSP에서 모두 구현하는 구조이다.** 

- 따라서 클라이언트 요청을 받는 것도 JSP, Model과 상호작용하여 변경된 Model 사용하여 View를 다시 그려내는 것도 JSP이다.
- 즉, 사용자 요청 처리와 응답 처리를 모두 JSP에서 구현하는 구조이다.

**2) Model2 는 Model1과 다르게 View와 Controller가 분리된 구조 가진다.**

- Controller와 View를 분리함으로써 클라이언트 요청 처리 부분과 응답 처리 부분을 분리하여 각 로직을 독립적으로 수행할 수 있다.

### **✅ MVC 패턴 규칙 (주의할 점)**

**1) Model은 Controller와 View 에 의존하지 않아야 한다.**

- 즉, Model 내부에 Controller와 View 관련 코드 있으면 안됨 오직 비즈니스 로직 처리에 집중

**2) View는 Model에만 의존해야 하고, Controller에는 의존하면 안된다.**

- View 내부에 Model의 코드만 있을 수 있고, Controller의 코드가 있으면 안된다.

**3) View가 Model로부터 데이터 받을 때는 사용자마다 다르게 보여주어야 하는 데이터에 대해서만 받아야 한다.**

**4) Controller는 Model과 View에 의존해도 된다.**

- Controller 내부에는 Model과 View의 코드 있을 수 있다.

**5) View가 Model로부터 데이터 받을 때 반드시 Controller 경유하여 받아야 한다.**

### **✅ 왜 MVC 패턴을 사용해야 하나요 ? | 장점**

1) 역할 명확히 분리하여 서로 간 결합도 낮출 수 있다.

2) 코드 재사용성 및 확장성 높인다.

3) 서비스 유지보수 테스트 용이해진다.

4) 개발자 간 커뮤니케이션 효율성 높일 수 있다.

### **✅ MVC 패턴 사용 시 단점은 ? | 단점 및 한계점**

프로그램이 복잡하고 대규모화되면 ‘Controller’ 너무 커진다.

개발 유지보수 용이하도록 설계된 모델임에도, 일정 수준 프로그램이 복잡해지면 수정 시 테스트 어렵고 하나의 수정이 다른 부분에 영향을 미치는 역효과도 있을 수 있다.

**[MVC 패턴의 한계]**

Model과 View가 서로의 정보를 갖고있지 않은 독립적 상태라곤 하지만, Controller를 통해 소통이 이뤄지기 때문에 의존성이 완벽히 분리될 수는 없다.

복잡한 대규포 프로그램의 경우 다수의 View 와 Model이 Controller를 통해 연결되기 때문에 되려 Controller가 불필요하게 커지는 현상이 발생한다.    **Massive-View-Controller 현상**

### **✅ MVC 패턴의 대안이 있나 ? [대안은 다른 패턴 사용]**

- MVVM 패턴 : 뷰와 모델 간 데이터 바인딩 쉽게 구현하고자 할 때, 뷰와 모델 간 의존성 해결하기 위해 MVVM 패턴 사용할 수 있다.
- FLUX 아키텍처 : 복잡한 애플리케이션에서 상태 관리 효과적으로 하고자 할 , Acrion과 상태를 이용하여 예측 가능한 데이터 흐름을 구현하고 자할 때 사용
- Redux 아키텍처 : 상태 관리를 중심으로 구현하고자 할 때 불변성을 강조하여 상태 관리 복잡성을 줄이고자 할 떄 사용

### **✅ MVC 패턴 사용하는 프레임워크나 라이브러리**

→ Spring Framework, Django, Angular JS  등 더 많다.

출처:

[https://velog.io/@yukina1418/모놀리식-아키텍처와-MSA](https://velog.io/@yukina1418/%EB%AA%A8%EB%86%80%EB%A6%AC%EC%8B%9D-%EC%95%84%ED%82%A4%ED%85%8D%EC%B2%98%EC%99%80-MSA)

https://devms.tistory.com/380

https://dev-coco.tistory.com/164

https://mangkyu.tistory.com/95

[MangKyu's Diary:티스토리]

https://lasbe.tistory.com/99

[https://devdange.tistory.com/entry/Web-Model1-Model2-MVC-패턴의-구조와-장단점](https://devdange.tistory.com/entry/Web-Model1-Model2-MVC-%ED%8C%A8%ED%84%B4%EC%9D%98-%EA%B5%AC%EC%A1%B0%EC%99%80-%EC%9E%A5%EB%8B%A8%EC%A0%90)

[https://velog.io/@come_true/WAS와-WS의-차이점](https://velog.io/@come_true/WAS%EC%99%80-WS%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90)

[https://medium.com/@heoh06/프론트엔트-기술면접-mvc-패턴-c0639999820a](https://medium.com/@heoh06/%ED%94%84%EB%A1%A0%ED%8A%B8%EC%97%94%ED%8A%B8-%EA%B8%B0%EC%88%A0%EB%A9%B4%EC%A0%91-mvc-%ED%8C%A8%ED%84%B4-c0639999820a)

https://codechasseur.tistory.com/25

