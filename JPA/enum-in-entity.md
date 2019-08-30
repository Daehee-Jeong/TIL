## JPA Entity에서 Enum 활용하기

최근 사내에서 혼자 개발중인 프로젝트에 JPA를 활용하여 개발을 하면서,
엔터티들이 갖는 각종 상태 값들의 저장에 대해 고민을 해보았습니다.

단순 **String** 형태로 선언 해놓은 어트리뷰트라면, *DB에서 유지관리 되는 형식에 맞춰 값이 들어오고 있는지* 에 대해서도 이슈가 있을 것입니다.

따라서 인터넷을 찾아보며 enum을 활용하여 이러한 작업에 있어 효율적으로 작업을 진행할 수 있었습니다.

## @Enumerated

Entity의 Attribute에 Enum을 사용하려면 해당 어트리뷰트 변수 위에 `@Enumerated` 애노테이션을 지정해주면 됩니다.

## EnumType.ORDINAL & EnumType.STRING

`@Enumerated` 애노테이션에는 **ORDINAL**과 **STRING**의 두가지 EnumType을 부여할 수 있습니다.

- `@Enumerated(EnumType.ORDINAL)` : Enum의 순서값을 DB에 저장합니다
- `@Enumerated(EnumType.STRING)` : Enum의 name을 DB에 저장합니다.

### 예시)
```java
public enum OrderStep {
    TEMPORARY,      /* 가주문 */
    PAYED,          /* 결제완료 */
    PREPARING,      /* 상품준비중 */
    SHIPPED         /* 발송완료 */
}
```

만일 Enum의 value를 `PAYED`로 지정하고 save했을 때

EnumType.ORDINAL의 경우 **1** 이라는 순번이 저장,
EnumType.STRING의 경우 **PAYED** 라는 네임 값이 저장됩니다.

이렇게 하여 Enum을 활용할 수 있지만, 아직 완벽해 보이지는 않는 것 같습니다.

**STRING**을 사용하자니 이러한 애트리뷰트가 많아진다면 DB에게도 무리를 주는 것 같고,
**ORDINAL**의 경우는 저장되는 실제값이 자바코드의 enum 밸류 순서에 의존하는 것 같아 정합성에 대한 불안함이 생깁니다.

따라서 이러한 부분에 대한 해소방법을 찾아보니 `Converter`를 사용하는 방법을 알게되었습니다.

JPA Entity에서 Enum 사용 방법에 대해서는 여기까지 정리하고, 문제점을 마저 보완하기위해 `Converter`를 사용한 내용은 별도로 글을 작성하도록 하겠습니다.

혹시 제 글에 잘못된 부분이 있다면 댓글 혹은 PR 주시면 감사하겠습니다.

___

>**수정이력**  
2019.08.30 최초작성