## Mastering Spring Web 101 Workshop (1일차)

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

