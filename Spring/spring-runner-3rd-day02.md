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