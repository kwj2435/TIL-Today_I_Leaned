1. InnerJoin
- Table A와 Table B에 대한 교집합을 조회

2. OuterJoin
- Table A와 Table B에 대한 합집합을 조회
- 조인 조건에 해당하지 않는 데이터를 함께 조회할 경우 사용

3. LeftJoin
  - 테이블 결과의 기준이 왼쪽 테이블 일 경우 
  ex) from member m leftjoin grade g on m.seq = g.memberId;
  이 경우 왼쪽에 있는 member가 조회의 기준이 된다. 
4. RightJoin
  - 테이블 결과의 기준이 오른쪽 테이블 일 경우 
ex) from member m rightjoin grade g on m.seq = g.memberId;
이 경우 grade가 조회의 기준이 된다. 
5. FullOuterJoin
  - 양쪽 테이블에 있는 데이터를 모두 보여준다.