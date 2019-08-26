## Spring Security 사용 시 Thymeleaf에서의 사용방법

`#authentication`은 Spring Security에서 `org.springframework.security.core.Authentication` 객체를 의미합니다.
<br>

따라서 다음과 같이 사용이 가능합니다.
```html
<p th:text="${#authentication.name}">
<p th:text="${#authentication.principal}">
<p th:text="${#authentication.principal.empNo}"><!--정의한 객체 멤버변수로 empNo가 정의되어있을 때의 예시-->
```
<br>

유저의 권한을 비교하기 위해서는 다음과 같이 작성하면 됩니다.
```html
<div th:if="${#authorization.expression('hasRole(''ROLE_ADMIN'')')}">
  ROLE_ADMIN이라는 권한을 가진 유저인 경우에만 다음 div태그가 보일것임
</div>

<div sec:authorize="hasRole('ROLE_ADMIN')">
  인증 된 사용자에게 ROLE_ADMIN 역할이있는 경우에만 표시됩니다.
</div>

<!-- 두 가지 예시 모두 동일하게 작동하겠지만 첫번째 방식을 이용하면 변수에 담아서 후처리하거나 아니면 비교시에 삼항연산자를 사용하는 등 다른 여러방식으로 사용이 가능하다. -->
```

___

>**수정이력**  
2019.08.26 최초작성

>**참고자료**  
https://github.com/thymeleaf/thymeleaf-extras-springsecurity