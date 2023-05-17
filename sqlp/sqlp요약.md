## 전문가가이드

1. 모델링의 특징

추상화 : 현실세계를 일정한 형식에 맞추어 표현을 한다는 의미

단순화 : 복잡한 현실세계를 약속된 규약에 의해 제한된 표기법이나 언어로 표현

명확화 : 누구나 이해하기 쉽게 대상에 대한 애매모호함을 제거

2. 모델링의 세 가지 관점

데이터관점 + 프로세스과점 + 데이터프로세스 상관관점

3. 데이터 모델링의 정의

정보시스템을 구축하기 위한 데이터 관점의 업무 분석 기법

현실세계의 데이터에 대해 약속된 표기법에 의해 표현하는 과정

데이터베이스를 구축하기 위한 분석,설계의 과정

4. 데이터 모델의 기능

명세화, 구조화, 문서화, 다양한 관점, 상세수준의 표현

5. 데이터 모델링의 중요성

파급효과(Leverage), 복잡한 요구사항의 간결한 표현(Conciseness), 데이터 품질(Data Quailty)

6. 데이터 모델링의 3단계

개념적 데이터 모델링 : 추상화, 업무중심적, 포괄적, 전사적, EA수립시 사용

논리적 데이터 모델링 : KEY, 속성, 관계 표현, 재사용성 높음

물리적 데이터 모델링 : 실제 DBMS에 이식, 물리적인 성격 고려

7. 데이터 독립성

논리적 독립성 : 개념스키마 변경, 외부스키마 영향 없음, 논리적 구조가 변경되어도 응용프로그램 영향없음

물리적 독립성 : 내부스키마 변경, 외부/개념스키마 영향 없음, 저장장치의 구조변경은 응용프로그램과 개념스키마에 영향없음

8. 사상

외부/개념적 사상(논리적 사상) : 외부적 뷰와 개념적 뷰의 상호 관련성 정의(개념적 뷰의 필드 타입은 변화 없음)

개념/내부적 사상(물리적 사상) : 개념적 뷰와 DBMS간의 상호 관련성 정의(DB구조 변경시 개념적/내부적 사상이 바뀌어야 개념적 스키마가 그대로 남음)

9. 데이터 모델링의 세가지 요소

어떤것(Things), 성격(Attributes), 관계(Relationships)

10. 데이터 모델 이해 관계자

DBA, 개발자(가장중요), 현업업무전문가, 전문 모델러

11. 좋은 데이터 모델 요소

완전성(Completeness)

중복배제(Non-Redundancy)

업무규칙(Business Rules)

데이터재사용(Data Reusuability)

의사소통(Communication)

통합성(Integration)

12. 엔터티의 특징

반드시 필요, 식별가능, 영속적으로 존재(두개이상), 업무프로세스 이용, 속성필수, 관계필수

13. 엔터티 분류

유무형 : 유형엔터티, 개념엔터티, 사건엔터티

발생시점 : 기본엔터티, 중심엔터티, 행위엔터티

14. 속성의 분류

기본속성(이름), 설계속성(코드), 파생속성(합계)

15. 주식별자의 특징

유일성, 최소성, 불변성, 존재성

16. 식별자 분류

대표성 여부 (주식별자, 보조식별자)

스스로생성 여부 (내부식별자, 보조식별자)

단일속성 여부(단일 식별자, 복합식별자)

대체 여부(본질식별자, 인조식별자)

17. 식별자/비식별자 관계

식별자 관계 : 부모로 받은 식별자를 자신엔터티의 주식별자로 이용

비식별자 관계 : 부모로 부터 속성을 받았지만 주식별자로 사용하지 않고 일반 속성으로 사용

18. 비식별자 관계 설정 고려사항

약한 관계, 독립 PK구성, PK속성 단순화를 위해서 고려

19. 식별자 관계 설정 고려사항

강한 관계, 주식별자 PK사용

20. 함수 종속성 이란?

데이터들이 어떤 기준값에 의해 종속되는 현상을 지칭한다.

기준값을 결정자, 종속되는 값을 종속자 라고 한다.

ex) 주민등록번호 -> (이름,출생지,주소)

21. 반정규화 기법

1) 테이블 반정규화

테이블 병합(1:1, 1:M, 슈퍼/서브타입), 테이블 분할(수직,수평), 테이블 추가(중복, 통계, 이력, 부분)

2) 칼럼 반정규화

중복칼럼 추가, 파생칼럼 추가, 이력테이블 칼럼 추가, PK에 의한 칼럼 추가, 응용시스템 오작동을 위한 칼럼 추가

3) 관계 반정규화

중복관계 추가

22. 슈퍼서브타입 모델

공통의 부분을 슈퍼타입으로 모델링, 다른 엔터티와 차이가 있는 속성에 대해서 별도의 서브 엔터티로 구분

1) OneToOne Tyle

개별테이블, 확정성 우수, 조인성능 나쁨, I/O 좋음, 관리안좋음

2) Plus Type

슈퍼서브타입테이블, 확정성 보통, 조인성능 나쁨, I/O좋음, 관리안좋음

3) Single Type

하나의 테이블, 확정성 나쁨, 조인성능 우수, I/O나쯤, 관리좋음

23. 분산 데이터베이스의 투명성

분할투명성, 위치투명성, 지역사상 투명성, 중복투명성, 장애투명성, 병행투명성

24. 분산 데이터베이스의 장단점

장점 : 지역자치성, 점증적시스템 용량확장, 신뢰성,가용성, 효용성, 융통성, 빠른 응답, 통신비용절감, 데이터가용성, 신뢰성, 시스템규모조절, 요구수용 증대

단점 : 비용, 오류잠재성증대,처리비용,설계관리복잡성,불규칙한응답속도,통제어려움,데이터무결성위협

25. 분산 데이터베이스 적용 기법

1) 위치분산

2) 분할분산 : 수평분할, 수직분할

3) 복제분산 : 부분복제(통합된건 본사, 각지사별로 해당로우), 광역복제(본사,지사모두 동일한 데이터 가지고있음)

4) 요약분산 : 분석요약(각지사별로 요약, 본사에 통합), 통합요약(각지사별로 존재하는 다른 내용이 정보요약, 본사에 통합)

26. 외래키 추가  SQL

ALTER TABLE PLAYER ADD CONSTRAINT PLAYER_FK FOREIGN KEY (TEAM_ID) REFERENCES TEAM(TEAM_ID);

27. 트랜잭션의 특성

원자성(Atomicity), 일관성(Consistency), 고립성(Isolation), 지속성(Durability)

28. 각종 함수 결과값

SELECT RTRIM('XXXYYY   ', ' ') FROM DUAL; -> "XXXYYY"

SELECT LTRIM('XXXYYY   ', 'X') FROM DUAL; -> ""YYY   "

SELECT SIGN(-00) FROM DUAL; -> "0"

SELECT SIGN(-100) FROM DUAL; -> "-1"

SELECT SIGN(100) FROM DUAL; -> "1"

SELECT CEIL(38.123) FROM DUAL; -> "39"

SELECT CEIL(-38.123) FROM DUAL; -> "-38"

SELECT FLOOR(38.123) FROM DUAL; -> "38"

SELECT FLOOR(-38.123) FROM DUAL; -> "-39"

SELECT ROUND(38.5235, 3) FROM DUAL; -> "38.524"

SELECT ROUND(38.5235, 1) FROM DUAL; -> "38.5"

SELECT ROUND(38.5235, 0) FROM DUAL; -> "39"

SELECT ROUND(38.5235) FROM DUAL; -> "39"

SELECT TRUNC(38.5235, 3) FROM DUAL; -> "38.523"

SELECT TRUNC(38.5235, 1) FROM DUAL; -> "38.5"

SELECT TRUNC(-38.5235, 1) FROM DUAL; -> "38.5"

SELECT TRUNC(38.5235, 0) FROM DUAL; -> "38"

SELECT TRUNC(38.5235) FROM DUAL; -> "38"

SELECT NULLIF('1', '1') FROM DUAL; -> 널

SELECT COALESCE(NULL, '2', '1') FROM DUAL; -> "2"

29. 뷰의 장점

독립성, 편리성, 보안성

30. 일반 집합연산자와 현재의 SQL 비교

UNION 연산은 UNION 기능으로

INTERSECTION 연산은 INTERSECT 기능으로

DIFFERENCE 연산은 EXCEPT, MINUS 기능으로

PRODUCT 연산은 CROSS JOIN 기능으로

31. 순수관계 연산자와 현재의 SQL 비교

SELECT연산은 WHERE절로 구현

PROJECT연산은 SELECT 절로 구현

NATURAL JOIN연산은 다양한 JOIN기능으로 구현

DIVIDE연산은 현재 사용되지 않는다.

32. 계층형 쿼리

순방향
```sql
SELECT

LEVEL, LPAD(' ', 4*(LEVEL-1)) || EMPNO, MGR, CONNECT_BY_ISLEAF

FROM EMP

START WITH MGR IS NULL

CONNECT BY PRIOR  EMPNO = MGR;
```

역방향

```sql
SELECT

LEVEL,

LPAD(' ', 4*(LEVEL-1))||EMPNO,

MGR, CONNECT_BY_ISLEAF

FROM EMP

START WITH EMPNO = 7876

CONNECT BY PRIOR MGR = EMPNO;
```

패스함수
```sql
SELECT

CONNECT_BY_ROOT EMPNO,

SYS_CONNECT_BY_PATH(EMPNO, '/') ,

EMPNO, MGR

FROM EMP

START WITH MGR IS NULL

CONNECT BY PRIOR EMPNO = MGR;
```

33. ROLL UP, CUBE, GROUPING SETS, GROUPING

```sql
SELECT

CASE GROUPING(DNAME) WHEN 1 THEN '모든부서' ELSE DNAME END AS DNAME,

CASE GROUPING(JOB  ) WHEN 1 THEN '부서별' ELSE JOB   END AS JOB,

--,

COUNT(*),

SUM(SAL)

FROM EMP, DEPT

WHERE EMP.DEPTNO =  DEPT.DEPTNO

--GROUP BY ROLLUP(DNAME, JOB)

--GROUP BY DNAME, ROLLUP(JOB)

--GROUP BY ROLLUP(DNAME, (JOB,MGR))

--GROUP BY CUBE(DNAME, JOB)

GROUP BY GROUPING SETS(DNAME, JOB)

ORDER BY DNAME, JOB;
```
34. RAC(Real Application Cluster)

여러 인스턴스가 하나의 데이터베이스를 액세스 할수 있다.

하나의 인스턴스가 여러 데이터베이스를 액세스 할수 없다.

042012

35. Fast Commit 매커니즘

사용자의 갱신내용이 메모리상의 버퍼 블록에만 기록된 채 아직 디스크에 기록되지 않았더라도

Redo로그를 믿고 빠르게 커밋을 완료, 인스턴스 장애가 발생하더라도 로그파일을 이용해 언제든

복구가 가능하므로 안심하고 커밋을 완료

36. Write Ahead Logging

버퍼 캐시 블록을 갱신하기 전에 변경사항을 먼저 로그 버퍼에 기록, Dirty 버퍼를 디스크에 기록하기

전에 해당 로그 엔트리를 먼저 로그 파일에 기록

37. Recursive Call

DBMS내부에서 발생하는 Call, SQL파시와 최적화 과정에서 발생하는 데이터 사전 조회,

사용자 정의함수/프로시저 내에서 SQL수행, 해당 콜을 최소화하기 위해서는 바인드변수 사용하여 하드파싱 줄이고,

사용자정의함수 및 프로시저의 무분별한 사용 금지

38. 사용자정의함수/프로시저 특징

사용자정의함수/프로시저는 내장함수처럼 native코드로 완전 컴파일된 형태가 아니어서

가상머신같은 별도의 실행엔진 사용, 실행될때마다 문백전환이 일어나며, 내장함수를

호출할때와 비교해 성능을 떨어뜨린다.

그러므로 소량의 데이터 일때 혹은 부분범위처리 상황에서 제한적으로 사용한다.
 

39. 트랜잭션의 특징

원자성, 일관성, 격리성, 영속성


40. 트랜잭션 격리성 수준 상향

set transaction isolation level read serializable;

41. snap shot too old 방지

udno 영역 크기 증가, 커밋 자주 X, fetch across commit X, 트랜잭션 시간 조정,

테이블 나누어 단계적으로 코딩, NL조인형태 지양, 소트연산 발생, 대량업데이트후 full스캔

42. Secondary 인덱스로부터 IOT레코드를 가리킬때

오라클은 Logical Rowid = PK + Physical Guess 를 사용한다.

Physical Guess = Secondary index를 최초 생성하거나 재생성한 시점의 Data block Address

Physical Guess를 찾아갔다가 없으면 PK로 탐색

43. 형변환

숫자형과 문자형이 만나면 -> 문자형을 숫자형으로 형변환

44. Direct Path Insert

insert select 문장에 /*+ append */ 힌트 사용

병렬모드 insert

CTAS 문장을 수행

* nologging 모드 Insert (Direct Path Insert모드일때만 사용가능)

alter table t nologging; -> redo 로그까지 최소화

림

주의사항 : Direct Path Insert시 테이블 Lock걸림

---------------------------------------------------------------------------------------------------------------------------

## 성능고도화
 

1. REDO 로그의 목적

A. Database Recovery

Media Fail 발생시 DBMS 복구

Archived Redo Log 이용

B. Cache Recovery

Instance Recovery 라고도 한다

버퍼캐시에 저장된 변경사항이 디스크에 저장 되지 않은채 정전이 발생하면 Online Redo Log를 읽어들여

마지막 체크포인트이후부터 사고 발생 직전 까지 수행되었던 트랜잭션 재현한다.

다른말로 Roll Forward 단계라고 한다.

C. Fast Commit

사용자의 갱신내용이 메모리상의 버퍼 블록에만 기록된채 아직 디스크에 기록되지 않았지만 Redo Log를 믿고 빠르게 커밋을 완료

2. Write Ahead Logging

버퍼 캐시에 있는 블록 버퍼를 갱신하기 전에 Redo 엔트리 로그버퍼에 기록해야 하며,

DBWR이 버퍼캐시로 부터 Dirty 블록들을 디스크에 기록하기 전에 먼저 LGWR이 해당 Redo 엔트리를

모두 Redo로그 파일에 기록했음이 보장되어야 한다.

3. Undo 로그의 목적

A. Transaction Rollback

트랜잭션에 의한 변경사항을 최종 커밋하지 않고 롤백하고자 할때 Undo 데이터를 이용

B. Transaction Recovery

Instance Crash 발생후 Redo를 이용해 Roll Forward 단계완료후 시스템이 셧다운 시점에 아직 커밋되지

않았던 트랜잭션들을 모두 롤백할때 Undo 세그먼트에 저장된 Undo데이터를 사용한다.


C. Read Consistency

읽기 일관성을 위해서 사용된다.

4. 문장 수준 읽기 일관성

단일 SQL문이 수행디는 도중에 다른 트랜잭션에 의해 데이터의 추가, 변경, 삭제가 발생하더라도

일관성있는 결과 집합을 리턴하는 것이다.

5. Consistent, Current 모드 읽기

SELECT는 Consistent 모드로 읽는다.

INSERT, UPDATE, DELETE, MERGE 는 Current 모드로 읽고 쓴다. 다만, 갱신할 대상 레코드를 식별하는 작업은 Consistent 모드로 이루어진다.

6. 블록 클린아웃

트랜잭션에 의해 설정된 Row Lock을 해제하고 블록헤더에 커밋 정보를 기록하는 오퍼레이션

A. Delayed 블록 클린 아웃

트랜잭션이 갱신한 블록 개수가 총 버퍼 블록개수의 10%를 초과시

ITL슬록에 커밋 정보저장하고 레코드에 기록된 Lock Byte 해제하고 Online Redo에 Logging

B. 커밋 클린아웃

Online Redo로그를 남기지 않고 로깅시점을 뒤로 미룬후 해당 블록을 갱신하려고 Current모드로 읽는 시점에

Lock Byte를 해제하고 완전한 클린아웃을 수행한다.
 
7. SnapShot too old 발생원인

A. 데이터를 읽어 내려가다가 쿼리 SCN이후에 변경된 블록을 만나 과거시점으로 롤백한

Read Consistent 이미지를 얻으려고 하는데 Undo블록이 다른 트랜잭션에 의해 재사용돼 필요한

Undo정보를 얻을수 없는경우 발생한다.

B. 커밋된 트랜잭션 테이블 슬롯이 다른 트랜잭션에 의해 재사용돼 커밋정보를 확인할수 없는 경우 발생한다. (Undo 세그먼트 개수가 적음)

8. Snap Shot too old 회피 방법

커밋 자주 하지 말것, 트랜잭션 몰리는 시간대를 피해서 돌린다, 큰 테이블을 일정위로 나눠서 작업,

오랜시간에 걸쳐 같은 블록을 여러번 방문하는 NL 조인 형태에서 인덱스를 경유한 테이블 액세스가 있는지 확인하여 풀 테이블 스캔 혹은 조인방식 변경으로 유도한다.

Order by를 강제로 삽입해 소트연산이 일어나도록 한다. Temp 세그먼트에 저장한후에는 아무리 같은 블록을 재방문하더라도 상관없다

대량의 업데이트후 곧바로 해당 테이블에 대해 Full Scan을 한번 날려준다.

9. 트랜잭션의 특징

원자성(Automicity), 일관성(Consistency), 격리성(Isolation), 영속성(Durability)

10. 트랜잭션 수준 읽기 일관성

트랜잭션이 시작된 시점을 기준으로 일관성있게 데이터를 읽어들이는 것을 말한다.

11. Autonomous Transaction

메인 트랜잭션에 영향을 주지 않고 서브 트랜잭션만 따로 커밋하는 기능

12. Latch

SGA에 공유되어 있는 갖가지 자료구조를 보호할 목적으로 사용하는 가벼운 Lock

13. Buffer Lock

버퍼 블록에 대한 액세스를 직렬화

14. 교착상태

두세션이 각각 Lock을 설정한 리소스를 서로 액세스 하려고 마주보고 진행하는 상황

15. Soft Parsing

메모리에 Caching되어 있는 SQL을 찾아서 바로 실행

16. Hard Parsing

메모리에서 SQL을 찾는데 실패해 최적화 및 Row-Source생성 단계를 거치는 것

17. 커서의 종류 정리

공유커서(Shared Cusor) : SGA내에 Shared Pool에 존재하는 라이브러리 캐시에 공유되있는 Shared SQL Area

세션커서(Session Cursor) : PGA내에 Private SQL Area에 저장된 커서

애플리케이션 커서(Application Cursor) : 세션 커서를 가리키는 핸들

18. 바인드변수 사용시 부작용

바인드 변수 사용시 통계정보는 활용, 컬럼 히스토그램 정보는 사용못함

19. 세션커서 캐싱

SQL구문 분석 후 해시값 계산, Liblary Lacth  획득한후 라이브러리 탐색 과정을 없애버린다.

20. 어플리케이션 커서 캐싱

세선커서 캐싱한 상태에서 공유커서 힙을 Pin하고 실행에 필요한 메모리 공간을 PGA에 할당하는 작업까지 없애버리낟.

범위 : 인덱스 원리와 활용

21. ROWID의 구성

데이터 오브젝트 번호(6자리) + 데이터파일 번호(3자리) + 블록번호(6자리) + 로우번호(3자리)

22. y.대상년월(+) = substr(x.파트너지원요청일자, 1,6) -1

x.파트너지원요청일자는 varchar2 형이다. varchar2 컬럼에 숫자 값을 더하거나 빼는 연산을 가하면

내부적으로 숫자형으로 형변환이 일어난다. 이럴 경우 y.대상년월 까지도 자동으로 형변환이 되므로

인덱스 스캔이 불가능해진다.

아래처럼 되는 것이다.

to_number(y.대상년월(+)) = to_number(substr(x.파트너지원요청일자,1, 6)) -1

이렇게 되므로 y.대상년월 컬럼의 인덱스가 먹히지 않는다.

아래와 같이 튜닝한다.

y.대상년월(+) = to_char(add_months(to_date(x.파트너지원요청일자, 'yyyymmdd') -1), 'yyyymm')

23. decode함수 사용시 주의점

decode(a, b, c, d) : a와 b가 같으면 c를 반환 아니면 d반환

여기서 c인자가 null값이면 varchar2로 취급한다.

그렇게 되면 d의 인자값을 varchar2로 형변환 시킨다.

max(decode(job, 'presidendt', null, sal)) max_sal2 -> 여기서 4번째 인자인 sal의 max값을 구할때 varchar2로 형변환 상태에서 max값을

구하므로 950이 3000보다 더 큰값이라고 잘못 나와 버린다.

아래와 같이 수정한다.

max(decode(job, 'president', to_number(null), sal)) max_sal2 -> 이렇게 하면 제대로 sal값의 max값이 나온다.

24. 비용 구하는 공식

비용 = blevel + (리프블록수 * 유효인덱스 선택도) + (클러스터링팩터 * 유효테이블 선택도)

25. IOT 적용할 테이블 유형

크기가 작고 NL조인으로 반복 룩업하는 테이블

폭이 좁고 로우수가 많은 테이블

넓은 범위를 주로 검색하는 테이블

데이터 입력과 조회패턴이 서로 다른 테이블

26. Physical guess

secondary index를 최초 생성하거나 재생성한 시점에 IOT레코드가 위치했던 데이터 블록 주소

27. Logical ROWID

Logical Rowid = PK + Physical guess

28. 비트맵 인덱스 를 스캔하면서 테이블 레코드를 찾아가는 방법

오라클은 한 블록에 저장할수 있는 최대 레코드수를 제한한다.

비트맵 인덱스 9500번째 비트가 1인 값의 레코드는?

최대레코드 개수는 : 730

9500/730 = 13 -> 14번째 블록

9500%730 = 10 -> 10번째 레코드

범위: 조인원리와 활용

39. 테이블 Prefetch

한번의 Disk I/O를 통해서 곧이어 읽을 가능성이 큰 블록들을 캐시에 미리 적재 하는 기능

40. 테이블 Prefetch 가 일어나는 상황

Inner쪽 Non-Unique 인덱스를 Range Scan할 때

Inner쪽     Unique 인덱스를 Non-Unique 조건으로 Range Scan 할때

Inner쪽     Unique 인덱스를 Unique조건으로 실행할때 나타날수있는데 이때는 Range Scan으로 액세스

41. Buffer Pinning 일어나는 상황

테이블 블록에 대한 Buffer Pinning

Inner쪽 인덱스 루트 블록에대한 Buffer Pinning

하나의 Outer레코드에 대한 Inner쪽과의 조인을 마치고 Outer쪽으로 돌아오더라도 테이블 블록에 대한 Buffer Pinning

User Rowid로 테이블 액세스시 Buffer Pinning

Inner쪽 루트아래 인덱스 블록들도 Buffer Pinng

42. 확장된 ROWID 포맷

데이터오브젝트번호(6)+데이터파일번호(3)+블록번호(6)+로우번호(3)

43. IOT 사용 상황

크기가 작고 NL조인으로 반복 룩업하는 테이블

폭이좁고 긴 테이블

넓은 범위를 주로 검색하는 테이블

데이터 입력과 조회패턴이 서로 다른 테이블

44. 인덱스 설계

조건절에 사용, '='조건으로 조회

45. QBNAME 힌트의 사용

```sql
SELECT /*+ LEADING(DEPT@QB1) */ *

FROM EMP

WHERE DEPTNO IN

(

SELECT /*+ UNNEST QB_NAME(QB1) */

DEPTNO

FROM

DEPT

)

;
```
 

46. NL_SJ 의 사용

```sql
SELECT /*+ LEADING(EMP) */

*

FROM EMP

WHERE DEPTNO IN

(

SELECT /*+ UNNEST NL_SJ */

DEPTNO

FROM DEPT

);
```

47. NL_AJ 의 사용

```sql
SELECT *

FROM DEPT D

WHERE NOT EXSITS

( SELECT /*+ UNNEST NL_AJ */ 'X'

FROM EMP

WHERE DEPTNO = D.DEPTNO

);         
```
 

48. NO_UNNEST와 PUSH_SUBQ의 사용

```sql
SELECT /*+ LEADING(E1) USE_NL(E2) */

SUM(E1.SAL), SUM(E2.SAL)

FROM EMP1 E1, EMP2 E2

WHERE E1.NO = E2.NO

AND EXISTS

( SELECT /*+ NO_UNNSET PUSH_SUBQ */ 'X' FROM DEPT

WHERE DEPTNO = E1.DEPTNO

AND LOC = 'NEW YORK'

);
```

49. 뷰머징이 되지 않는 상황

집합연산자, CONNECT BY 절, ROWNUM 사용, GROUP BY 없이 집계함수 사용, 분석함수

50. 병렬 DML 처리

```sql
ALTER SESSION ENABLE PARALLEL DML;

EXPLAIN PLAN FOR

UPDATE /*+ PRRALLEL(T 4) T SET NO2 = LPAD(NO, 5, '0');

ALTER SESSION ENABLE PARALLEL DML;

INSERT /*+ APPEND PARALLEL(T1 4) INTO T1

SELECT /*+ FULL(T2) PARALLEL(T2 4) */ * FROM T2;
```
 

51. Granule

블록기반 Granule : PX BLOCK ITERATOR

파티션기반 Granule : PX PARTITION RANGE ALL(파티션 전체), PX PARTITION RANGE ITERATOR(부분 파티션)

52. 파티션 조인

- FULL PARTITION WISE 조인 : 두개의 테이블이 같은 기준으로 파티셔닝 되어 있는 경우

- PARTIAL PARTITION WISE 조인 : 둘중 하나만 파티션 되어 있는 경우

- 동적 파티셔닝 : 양쪽 테이블을 동적으로 파티셔닝하고서 FULL PARTITION WISE 조인, 한쪽테이블을 BROADCAST 하고 나서 조인

- BROADECAST 방식

53. 카디널리티 구하는 공식

카디널리티 = 선택도 * 전체레코드 수

54.  세션 커서 캐싱

sql구문분석,해시값계산,라이브러리캐시 래치 획득,라이브러리커서 탐색 들을 생략                                         

55. 어플리케이션 커서 캐싱

세션커서캐싱에다가 공유커서 힙을 pin하고 실행에 필요한 메모리 공간을 pga할당하는 과정을 생략 

출처 : https://blog.naver.com/oracledo/220390350995
