## JVM 이란?
>자바 가상머신으로 자바 바이트 코드를 실행할 수 있는 주체

<br>

JVM 역할
- 실행될 클래스 파일을 메모리에 로드 후 초기화 작업 수행
- 메서드와 클래스변수들을 해당 메모리 영역에 배치
- 클래스로드가 끝난 후 JVM은 main메서드를 찾아 지역변수, 객체변수, 참조변수를 스택에 쌓음
- 다음 라인을 진행하면서 상황에 맞는 작업 수행(함수 호출, 객체 할당 등)
<br>

___

## JVM 구성

JVM 구성은 크게 4가지로 나눌 수 있습니다.
```
Class Loader, Execution Engine, Garbage Collector, Runtime Data Area
```
<br>

- Class Loader
    JVM 내로 class 파일을 로드하고 Link 작업을 통해 배치 등의 작업을 한다. 런타임시에 클래스를 로드한다.
<br>

- Execution Engine
    Class Loader를 통해 JVM 내부로 넘어와 Runtime Data Area(JVM 메모리)에 배치된 Byte code들을 명령어 단위로 실행시킨다.
<br>

- Garbage Collector
    생성된 객체의 생존 여부를 판단하여, 더이상 참조되지 않거나 null 인 객체의 메모리를 해체시켜 메모리를 반납한다. 
<br>

___

## Runtime Data Area

Java 어플리케이션을 실행하면서 할당받은 메모리 영역. Class Loader에서 준비한 데이터들을 보관하는 저장소.


```
Method(Static) Area, Heap Area, Stack Area, PC Register, Native Method Stack
*총 5개 요소로 구성
```
<br>

- Method(Static) Area
    - JVM이 읽어들인 클래스와 인터페이스 대한 런타임 상수 풀, 멤버 변수(필드), 클래스 변수(Static 변수), 생성자와 메소드를 저장하는 공간이다.

    - Runtime Constant Pool
        - 메소드 영역에 포함되지만 독자적 중요성이 있다.
        - 클래스 파일 constant_pool 테이블에 해당하는 영역이다.
        - 클래스와 인터페이스 상수, 메소드와 필드에 대한 모든 레퍼런스를 저장한다.
        - JVM은 런타임 상수 풀을 통해 해당 메소드나 필드의 실제 메모리 상 주소를 찾아 참조한다
<br>

- Heap Area
    - JVM이 관리하는 프로그램 상에서 데이터를 저장하기 위해 런타임 시 동적으로 할당하여 사용하는 영역이다.
    - New 연산자로 생성된 객체 또는 객체(인스턴스)와 배열을 저장한다.
    - 힙 영역에 생성된 객체와 배열은 스택 영역의 변수나 다른 객체의 필드에서 참조한다.
    - 참조하는 변수나 필드가 없다면 의미 없는 객체가 되어 GC의 대상이 된다.
    - 힙 영역의 사용기간 및 스레드 공유 범위
        - 객체가 더 이상 사용되지 않거나 명시적으로 null 선언 시
        - GC(Garbage Collection) 대상
        - 구성 방식이나 GC 방법은 JVM 벤더마다 다를 수 있다.
        - 모든 스레드에서 공유한다.
<br>

- Stack Area
    - 각 스레드마다 하나씩 존재하며, 스레드가 시작될 때 할당된다.
    - 메소드를 호출할 때마다 프레임(Frame)을 추가(push)하고 메소드가 종료되면 해당 프레임을 제거(pop)하는 동작을 수행한다.
    - 선입후출(FILO, First In Last Out) 구조로 push와 pop 기능 사용
    - 메소드 호출 시 생성되는 스레드 수행정보를 기록하는 Frame을 저장
    - 메소드 정보, 지역변수, 매개변수, 연산 중 발생하는 임시 데이터 저장
    - 기본(원시)타입 변수는 스택 영역에 직접 값을 가진다.
    - 참조타임 변수는 힙 영역이나 메소드 영역의 객체 주소를 가진다.
<br>

- PC Register
    - 현재 수행 중인 JVM 명령 주소를 갖는다.
    - 프로그램 실행은 CPU에서 인스트럭션(Instruction)을 수행.
    - CPU는 인스트럭션을 수행하는 동안 필요한 정보를 CPU 내 기억장치인 레지스터에 저장한다.
    - 연산 결곽값을 메모리에 전달하기 전 저장하는 CPU 내의 기억장치
<br>

- Native Method Stack Area
    - 자바 외 언어로 작성된 네이티브 코드를 위한 Stack이다.
    - 즉, JNI(Java Native Interface)를 통해 호출되는 C/C++ 등의 코드를 수행하기 위한 스택이다. 
    - 네이티브 메소드의 매개변수, 지역변수 등을 바이트 코드로 저장한다.
<br>

___

>**참고한 자료**  
https://hoonmaro.tistory.com/19  
https://qlyh8.tistory.com/178  
https://jeong-pro.tistory.com/148  

>**수정이력**  
2019.08.07 최초작성