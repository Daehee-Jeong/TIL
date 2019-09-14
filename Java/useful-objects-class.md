# 유용한 Objects class 사용법

최근 Objects 클래스의 메서드 사용을 자주 마주치게 되었습니다.

운영중인 시스템에서도 Objects 클래스 메서드들을 적용해보며 유용하다고 생각됐던 부분들을 정리하고자 합니다.

## 1. equals()

```java
Objects.equals(str1, str2);
```
예상하듯 str1과 str2이 같은지의 여부에 대해 boolean 값을 반환합니다.

다음 코드와 비교해보겠습니다.

```java
str1.equals(str2);
```

다음코드의 목적도 str1과 str2를 비교한 결과를 얻는 것입니다.
하지만 str1이 null일 때는 해당 메서드 수행시 **NPE**가 발생할 것 입니다.

따라서 **null의 경우도 포함하여 처리**를 할때 유용하게 사용 가능합니다.

## 2. isNull(), isNonNull()

개인적으로 이 두가지 메서드를 통해서 코드 가독성이 많이 높아졌다고 생각합니다.

Optional을 통해서 Null 컨트롤을 할 수도 있겠지만, 기존의 코드들을 그대로 두고 보았을 때, `if (something != null)` 또는 `if (something == null)` 이러한 방식으로 도배된 수많은 코드들은 다음과 같이 읽기 좋은 코드로 변형이 가능합니다.

```java
if (Objects.isNull(something)) {
    ...
}
/* 또는 */
if (Objects.isNonNull(something)) {
    ...
}
```

여러 조건을 동시에 비교할 경우에도 더 가독성을 높힐 수 있을 것이라고 생각합니다.

## 3. requireNonNull()

null이 들어오면 안될 상황에 대해 수동적으로 검사를 하고, Exception을 내는 식의 코드를 작성한 경험이 종종 있었습니다.

위 메서드 사용을 통해서 값이 존재한다면 초기화를하고, 아닐 시에는 NPE를 발생시키도록 하는 코드의 작성을 더욱 용이하게 해줍니다.

```java
/* str이 null이라면 NPE를 발생시키고, 값이 존재한다면 newStr을 초기화한다 */
String newStr = Objects.requireNonNull(str);
```

변형으로 아래와 같이 사용하는 것도 가능합니다.

```java
/* NPE를 던지지 않고 대체 값을 부여하는 방법 */
String newStr = Objects.requireNonNull(str, "default value");

/* NPE를 던지지 않고 정의한 동작(람다식)을 수행하는 방법 */
String newStr = Objects.requireNonNull(str, 
    () -> {
        System.getProperty("com.daehee.~~~") // 값이 null일때는 람다식을 수행
    }
);

```

___

>**참고한 자료**  
https://multifrontgarden.tistory.com/205  
https://thebook.io/006985/ch05/01/09/

>**수정이력**  
2019.09.14 requireNonNull 내용 추가  
2019.09.11 최초작성