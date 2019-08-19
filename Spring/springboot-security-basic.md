`spring-boot-starter-security`모듈을 활용해 springboot 프로젝트에 spring security를 적용하는 기본적인 방법을 정리하고, 함께 개념들을 정리하도록 하겠습니다.

## Spring Security란

Spring Security란 스프링 기반의 어플리케이션의 보안(인증과 권한)을 담당하는 프레임워크입니다.

다시말해 인증 전반에 걸쳐 기존에 일일이 개발하였던 부분(로그인, 사용자 인증, 프로그램 각각의 기능에 대한 권한 체크 등)에 대한 작업을 미리 구현해 놓은 프레임웍이라고 할 수 있습니다.

프로그램외에도 리소스(이미지 등)에 대한 접근제어, `CSRF(Cross Site Request Forgery)` 공격 방어, `세션 고정(Session Fixation) 공격` 방어 및 다중 접속 방지 등을 간단하게 구현할 수 있습니다.

## Spring Security 구조

![Spring Security 구조](/images/springboot-security-basic-01.png)

**절차설명**
1. HTTP 요청을 받는다.
2. **AuthentificationFilter**가 인증요청을 수신하고 인증 오브젝트를 만든다. (`AuthenticationToken`)
3. Token 객체를 생성 한 후 AuthenticationManager 의 인증 메소드 를 호출하는 데 사용
4. AuthenticationProvider로 인증 시도
5. ~ 7. User객체를 조회
8. 성공시 인증객체 반환 또는 실패시 AuthenticationException 발생
9. 인증 완료. AuthenticationManager는 완전히 채워진 인증객체를 관련 인증 필터로 되돌린다.
10. SecurityContext에서 인증 객체 저장

## spring-boot-starter-security

___

>**수정이력**  
2019.08.13 최초작성

>**참고자료**  
https://offbyone.tistory.com/88  
https://sjh836.tistory.com/165  
https://springbootdev.com/2017/08/23/spring-security-authentication-architecture/