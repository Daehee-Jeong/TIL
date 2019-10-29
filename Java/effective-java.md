## 이펙티브 자바 3/E 내용 정리

### Item 1. 생성자 대신 정적 팩터리 메서드 고려

정적 팩터리 메서드(static factory method)란 해당 클래스의 인스턴스를 반환하는 단순한 정적 메서드.

책에서는 `boolean` 타입의 Boxed class `Boolean`에서 예를 찾고 있다.

```java
public static Boolean valueOf(boolean b) {
    return b > Boolean.TRUE : Boolean.FALSE:
}
```

팩터리 메서드 사용은 장/단점을 가진다.

우선 장점부터,

#### 장점-1) 이름을 가질 수 있다.
생성자에 넘기는 매개변수와 생성자 자체만으로는 반환객체 특성 설명이 어렵다. **반환 객체에 대한 명시적 기능 설명에 훨싼 용이**하다.
-> 입력 매개변수들의 순서를 다르게 한 생성자를 추가? -> 생성자들의 정확한 역할을 기억하기 어렵고 실수가 발생한다.

#### 장점-2) 호출될 때마다 인스턴스를 새로 생성하지는 않아도 된다.
예시인 `Boolean.valueOf(boolean)`의 경우에도 객체를 아예 생성하지 않는다.
즉 불필요한 객체 생성을 막을 수 있고, 생성 비용이 큰 객체의 경우 성능에도 좋다.
(비슷한 기법이라고 하는 ***플라이웨이트 패턴*** 에 대해서도 알아보자)

#### 장점-3) 반환 타입의 하위 타입 객체를 반환할 수 있는 능력이 있다.
**반환할 객체의 클래스를 자유롭게 설정**할 수 있는 장점.

```java
public class Car {
    private String carName;
    private static Car carInstance;

    public Car() {}

    public Car(String carName) {
        this.carName = carName;
    }

    public static Car getCar(String carName) {
        if ("palisade".equals(carName)) {
            return new Palisade();
        } else if ("venue".equals(carName)) {
            return new Venue();
        }

        return carInstance != null ? carInstance : new Car();
    }

    public String getCarName() {
        return this.carName;
    }
}

class Palisade extends Car {
    public Palisade (String carName) {
        super(carName);
    }
}

class Venue extends Car {
    public Venue (String carName) {
        super(carName);
    }
}
```

위와 같은 예시가 있다고 가정할 때,

```java
Car.getCar("palisade").getCarName(); // 하위 객체 Palisade를 반환하고 부모클래스의 메서드 수행
Car.getCar("venue").getCarName(); // 하위 객체 Venue를 반환하고 부모클래스의 메서드 수행
```

#### 장점-4) 입력 매개변수에 따라 매번 다른 클래스의 객체를 반환할 수 있다.
예시로 `EnumSet`의 경우 원소가 64개 이하면 `RegularEnumSet`을, 원소가 65개 이상이면 `JumboEnumSet`의 인스턴스를 반환한다.
클라이언트는 팩터리가 건네주는 객체가 어느 클래스의 인스턴스인지 알 필요 없다.

#### 장점-5) 정적 팩터리 메서드를 작성하는 시점에는 반환할 객체의 클래스가 존재하지 않아도 된다.
반환되는 것은 인터페이스이기 때문에 당장은 반환할 객체의 클래스가 존재하지 않아도 된다. 구현은 자손클래스가 한다.

#### 단점-1) 상속을 하려면 public이나 protected 생성자가 필요하기 때문에 정적 팩터리 메서드만 제공하면 하위 클래스를 만들 수 없다.
(상속시 오류에 대해 정리하기)

#### 단점-2) 정적 팩터리 메서드는 프로그래머가 찾기 어렵다.

___


### Item 2. 생성자에 매개변수가 많다면 빌더를 고려하라

정적 팩터리와 생성자 둘다 제약이 존재 -> **선택적 매개변수가 많을 때** 대응 어려움

이러한 경우의 생성자 또는 정적 팩터리는 **점층적 생성자 패턴**이 종종 사용된다.
-> 점층적 생성자 패턴은 ***확장이 어렵다***(1개, 2개, ..., n개)
-> 또한 클라이언트 ***코드를 작성하거나 읽기 어렵다***

점층적 생성자 패턴 이외에 두 번째 대안 ***자바빈즈 패턴(JavaBeans pattern)***
-> 매개변수가 없는 생성자를 만든 후 **setter**를 호출해서 매개변수 값 설정
-> **일관성이 깨지고**, **불변으로 만들 수 없음**(*불변으로 만들 수 없는 부분에 대해 예시 작성하기)
-> 객체 하나를 만들기 위해 **여러번의 메서드 호출**
-> 객체가 완전히 생성되기 전까지 **일관성이 무너짐**

**빌더 패턴(Builder pattern)**
- 불변으로 작성 가능
- 빌더의 세터 메서드는 빌더 자신을 반환하기 때문에 연쇄 호출 가능 (***method chaining***)
- 계층적으로 설계된 클래스와 함께 쓰기에 좋다 (Pizza 추상클래스와 NyPizza, Calzone 예시 떠올리기)
- **Lombok**의 `@Builder`도 확인해보자
- 객체만들기 위해 빌더부터 만들어야 하는 부분이 단점이 될 수 있다.
- 매개변수가 최소 4개 이상은 되어야 값어치 함