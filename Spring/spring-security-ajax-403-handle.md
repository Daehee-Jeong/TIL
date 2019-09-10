## Spring Security AuthenticationEntryPoint 인터페이스 구현을 통해 인증되지 않은 ajax 요청에 대해 응답하기

Spring Security를 설정하여 사용하면 사용자가 인증되지 않은 상태로 특정 페이지에 접근시 설정된 Login 화면으로 돌려보냅니다.

이때 ajax로 REST API 요청을 한 경우라면, 인증되지 않은 요청이 들어올 경우 오류로 응답을 돌려주어야 맞는데 200상태코드와 함께 Login화면의 html전문을 텍스트로 응답을 받게 됩니다.

이러한 상황을 해결하기 위해서는 `AuthenticationEntryPoint` 인터페이스를 구현 및 설정하여 원하는 동작(인증되지 않은 rest api 요청 시 오류로 응답을 주기)을 구현할 수 있습니다.

`AuthenticationEntryPoint` 인터페이스에서
```java
commence(httpServletRequest, httpServletResponse, authenticationException)
```
메소드를 통해 response에 결과로 반환할 내용을 작성하여 넘기면 됩니다.

인터페이스를 구현하고 나면 Security Config에 주입받고 설정해주면 됩니다.
```java
http.exceptionHandling().authenicationEntryPoint(entryPointHandler);
```

이렇게 구현을 완료하고 나면 인증되지 않은 rest api 요청에 대해서
Login폼을 200코드로 리턴하는 것이 아닌 에러응답을 리턴할 수 있습니다.