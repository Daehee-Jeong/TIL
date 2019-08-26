## Mastering Spring Web 101 Workshop (2일차)

### 오전

Spring Boot가 가지고 있는 basic error controller가 가지고있는 기본에러화면을 노출하는 기능에서 커스텀 에러화면을 출력, 또한 오류코드에 따라 처리

아직 스프링 내부의 오류메세지가 그냥 나가고있음. 사용자 친화적인 오류 처리가 필요하다.

전체가 아닌 원하는 기능만 살짝 감싸는 것. 데코레이터 패턴

부트가 가지고있는 오류에대한 기본전략을 버리고 새로운 전략을 사용하도록,
의존성 주입에 대한 활용

WebMvcConfiguration 에서 ErrorAttributes 주입
messages.properties 정의
ReadableErrorAttributes 정의 및 우선순위 지정

Spring내 모든 Validation 결과는 BindingResult에 저장된다
규칙에 의해 추출된 값이 message source resolvable에 들어있다

국제화
메세지를 변환할때 코드를 넘기고 Locale을 넘기고 있다.
Locale: 사용자 브라우저의 언어
이미 Locale을 보면 사용자의 언어를 알 수 있다.
Locale 기반으로 메세지를 치환해서 작성해줄 수 있도록 되어있기 때문에 그 부분만 작성을 하면 된다.

messages_{locale}.properties 이건 스프링의 Convention !
LocalResolver가 동작하고 있기 때문에 설정에 따라 동작하는 것이다.
한가지 언어만 쓸 경우는 FixedLocalResolver라는 구현체를 구현하면 된다.
-> 어떤 경우일까? 요청에 따라(국가에 따라) 아예 service region을 나눠놓은 경우 등
-> 어플리케이션을 올릴때 파라미터식으로 들어갈 것

### 오후

로그인 구현
HttpServletRequest를 사용하는 것이 원시적 방법
Spring은 Servlet스펙을 최대한 사용하지 않도록 구성

HttpServletRequest -> WebRequest

@Valid 애노테이션 사용 시, BindingResult를 함께 받으면 개발자가 처리할 수 있도록 컨트롤러 안으로 결과와 함께 통과시킨다.

오류메세지 치환기능에 있어 중복코드가 발생하기 시작했음
ExceptionMessageTranslator 참고해서 리팩토링 필요

@ExceptionHandler는 해당 컨트롤러 안에서만 사용된다.
전역에서 이러한 기능을 사용하고 싶으면 @ControllerAdvice와 함께 사용해야한다.

ArgumentResolver를 추가하여 새로운전략을 Spring에게 알려줌

요청과 응답 가로채기
서블릿 필터 이용

인터셉터를 추가해서 rolesallowed인지를 확인하고 비교 등 수행

일일이 role allowed를 추가하기는 힘듬
Controller 자체에 획득

Filter를 통해서 http servlet request를 감싸는 작업을 왜하는지?

파일업로드에도 수평확장 이슈가 있다
어디에다가 올려야하지?

text/event-stream ?
서버입장에서는 SSE인지 아닌지 관심이 없음
HTML5 스펙상에서 eventSource라는 객체로만 접근 관리 하면 된다.