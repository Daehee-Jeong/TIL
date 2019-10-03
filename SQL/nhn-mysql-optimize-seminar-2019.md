## NHN MySQL 최적화 세미나 내용정리

- 실습 환경: `MySQL Workbench` (미리 구성되어있는 DB에 참가자 별로 계정을 부여받고 접속)
<br/>

- 강의 목차
    1. JOIN
    2. INDEX
    3.
<br/>

### 1. JOIN

주문과 상품을 예시로 릴레이션에 대한 사전지식이 설명되었다.

**N:M**의 케이스는 정규화된 테이블 구성에서는 발견되지 않는다.

ex) 2015년 이후 생성된 부서명과 사원명을 조회하라

ex) 2016년 이후 입사자가 있는 부서 리스트 조회

ex) 사원이 없는 부서 리스트 조회

Semi Join
조인되는 행의 개수와 상관없이 Outer 테이블의 결과를 추출하는 Join 방법

Nested Loop Join
- MySQL에서 지원하는 유일한 조인 방식
- 순차적인 처리를 하며, 먼저 처리되는 테이블의 처리 범위에 따라 전체 쿼리의 비용이 결정됨
- 조인에 참여하는 레코드 건 수가 많아질수록 전체적인 응답 속도 저하가 발생
- 조인 연결고리 칼럼에 인덱스 구성이 되어 있지 않은 경우 Lookup 회수만큼 Full Table Scan을 해야 함
- 다량의 Random I/O가 발생
- 주로 좁은 범위 처리에 유리

ex) 부서 100개, 사원 10,000명 있다면 어떤 테이블이 먼저 driving 될까 ?
```SQL
SELECT
    부서코드, 부서명, 사원번호, 사원명
FROM
    부서 A, 사원 B
WHERE A.부서코드 = B.부서코드
```

-> 부서코드를 가지고 후행테이블을 하나하나 찾는다. -> 100 * 10,000
-> 답: 사원테이블이 먼저 driving (scanning) 된다. (10000 * 1)


* 조인 순서의 결정
    1. 기본적으로 MySQL 옵티마이저는 모든 테이블 조인 순서에 대해서 Cost를 계산
    2. Cost 측정 방법은 단일 쿼리의 측정 방법과 동일
    3. 최소 Cost가 계산된 조인 순서를 기반으로 실행 계획 생성
<br/>

* 1 : N Join 시 튜닝
    • Parent(1) / Child(N) 를 확인
    • SELECT 절에 속한 컬럼 확인
    • 모두 PARENT에만 속하는 경우 중복제거를 위한 ( inner / left outer ) group by 혹은 distinct를 사용하는지 확인하여
    • SEMI JOIN 형태로 변경
<br/>

* 게시판 목록화면 (글과 댓글수를 보여주는) 예시
    - ㅁㄴㅇ

```SQL
SELECT a.prod_cd, a.prod_nm
FROM prod a INNER JOIN ordr_prod b ON a.prod_cd = b.prod_cd
WHERE a.prod_rgst_ymdt < ‘2016-07-01 00:00:00’
GROUP BY a.prod_cd, a.prod_nm ;
```

- 한개의 테이블에서만 select를 하고있고, 집계함수가 없는데 GROUP BY를 썼다는 점에서 중복제거를 위해썼다는 걸 알 수 있다
- 따라서 세미조인을 사용하는 것이 좋다

* 인덱스 구조
    - B-Tree 다 !
    - leaf node는 링크드리스트다 !!


* 인덱스 순서
    - 이퀄조건은 좌측으로 배치, range 조건 또는 order group은 우측으로 배치

* MySQL은 `null`이 인덱싱이 된다