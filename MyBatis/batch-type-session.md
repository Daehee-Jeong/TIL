## 대용량 엑셀파일(약1만 건 이상) 업로드 기능 개선을 위해 확인한 내용

SqlSession의  Default ExcutorType은 `ExcutorType.SIMPLE`이다.

기본 타입의 세션으로 1만건의 row를 insert 한다면
1만 번의 SqlSession을 create하고, flush, commit하는 과정을 반복하게 된다.

이 부분에서 굉장한 속도 저하가 생기게 되는데

SqlSession을 추가적으로 하나 더 생성하고 타입을 `ExcutorType.BATCH`로 선언한 뒤,
DAO의 반복되는 Loop를 배치세션을 사용해서 insert를 반복하게되면

이미 Fetch되어있는 세션을 그대로 얻어와 지속적으로 작업하고, 모든 작업을 마무리하고나서 flush 및 commit을 하게되어 속도가 매우 빨라진다.

___

>**수정이력**  
2019.08.10 최초작성