## Mastering Spring Web 101 Workshop (1일차)

### 오전

배경지식
웹애플리케이션, HTTP
HTTP 메서드 총 9가지..

GET
멱등성

POST
GET과의 차이는 Entity Body, 요청라인에서의 정보가 아님

HTTP Status Code

HTTP Header & Body

URL
자원 위치 주소규약

___

서블릿 기본

Java Servlet, JSP 개념

간단한 웹애플리케이션 구현 예제

Servlet은 기본적으로 HttpServlet을 상속 등
서블릿 인터페이스의 내용 들여다보기

Servlet은 기본 인코딩이 UTF-8로 설정되어있지 않기 때문에 req, resp에 설정을 먼저 진행

@WebServlet 어노테이션

ComponentScan -> Servlet은 탐색을 하지 않기때문에 추가적으로 어노테이션 설정 (@ServletComponentScan)

Boot Dashboard 패널

STS에서는 build.gradle에 대한 Sync를 지원하지 않음

Servlet Contianer 구성 확인
네트워크 통신제어, 스레드 기반 병렬처리
서블릿과 JSP의 생명주기 확인

___

스프링

Spring Boot 2.0
리액티브 스택, 서블릿 스택

대량요청 받는 서비스의 경우에 리액티브 스택
비동기 처리

POJO 스프링 3대 주요기슬이 POJO 프로그래밍을 돕는다.

DI,
AOP,
PSA

기존에는 applicationContext.xml로 스캔할 컴포넌트들에 관리

Spring Web MVC
애노테이션 기반 프로그래밍
자바의 애노테이션과 리플렉션 API 적극 사용
CoC (Convention of Configuration, 설정보다 관례)

프론트 컨트롤러 패턴과 웹 MVC 패턴

애노테이션
빌트인과 커스텀으로 분류

리플렉션 API

스프링부트
스프링 기반 단독실행 및 즉시 운영가능한 애플리케이션 개발
최소한의 설정으로 개발 구동
제안된 스프링플랫폼과 서드파티 라이브러리 사용으로 생산성 증대

starter들을 이용해서 web, batch, security 등등 이용할 수 있음

cli는 안씀

tools - ex devtools ...

Getting Started 프로젝트 기본 소스 확인

Spring Boot도 마찬가지로 메인메서드가 호출되면서 프로그램 시작

스프링 부트 웹 자동 구성 확인

Servlet Filter
Spring Web MVC
Spring
Embedded Servlet Container
JVM

___

### 오후

제공된 애플리케이션 정의서를 바탕으로 프로젝트 작성

인증과 인가의 차이
Authentication & Authority

아키텍처 (멀게 느껴지는 정의)
- 요소: 모듈, 컴포넌트, 클래스 (가 어떻게 관계를 가지는지)
- 관계
- 설계
- 진화의 원칙
을 포함한 것

아키텍처 (가깝게)
시스템 구성요소 원칙하에 분리
구성요소간 상호작용 방법에 대한 것

Architecture Pattern / Style

자바 가장많이 -> 계층화 (Layers Architecture Pattern)
Presentation / Domain / Data

포트 및 어댑터 아키텍처 (Ports and adapters architecture, a.k.a. hexagonal architecture)

아키텍처들의 공통점
세부사항으로 부터 애플리케이션을 떨어뜨리겠다

모델-뷰-컨트롤러 아키텍처 패턴

스케일 아웃, 수평 확장
ex 웹 서버의 수를 늘려 처리량을 증가

스케일 업, 수직 확장
ex 웹 서버의 하드웨어를 업그레이드해 처리량을 증가

Traditional Application (Multi-page Application)
<-> Single-page Application, SPA

실시간 유저 카운팅
-> 일정시간 마다 요청 X
-> HTML5 새로운 스펙(Server-Sent Event), 서버가 실시간으로 push를 줄 수 있음

Hikari CP ?

properties 사용하지않고 yaml 사용하는 이유
UTF-8 인코딩했을때 깨지지 않음
훨씬 축약된 형태로 사용 가능

slf4j

boot에서는 webapp폴더는 빌딩 중 버려진다. 유의미하지 않다.

리소스는 URI 표준에 따라서 불러질 수 있다.

