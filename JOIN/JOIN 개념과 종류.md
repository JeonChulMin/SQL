# JOIN

- JOIN은 여러 테이블 간에 공통된 컬럼을 기준으로 데이터를 합쳐 표현하는 것이다.
- INNER JOIN과 OUTER JOIN이 있다.
- 내부 조인은 쉽게 설명하면 두 테이블이 있을 경우 두 테이블에 공통적으로 있는 컬럼을 이용해 두 테이블을 연결하여 결과를 생성하는 방법이다. 
- WHERE절에서 같은 조인 조건에서 동등 연산자 `=`를 사용한 조인을 동등 조인(EQUI JOIN)이라고 한다.
- 예제를 위해 Oracla에서 제공되는 기본 테이블 DEPT, EMP 테이블을 활용해서 연습.



### [DEPT 테이블]

| Table | Column | Data Type | Length | Precision | Scale | Primary Key | Nullable                                                   | Default | Comment |
| ----- | ------ | --------- | ------ | --------- | ----- | ----------- | ---------------------------------------------------------- | ------- | ------- |
| DEPT  | DEPTNO | NUMBER    | -      | 2         | 0     | 1           | -                                                          | -       | -       |
|       | DNAME  | VARCHAR2  | 14     | -         | -     | -           | ![nullable](http://127.0.0.1:8080/i/check_small_black.gif) | -       | -       |
|       | LOC    | VARCHAR2  | 13     | -         | -     | -           | ![nullable](http://127.0.0.1:8080/i/check_small_black.gif) | -       | -       |



### [EMP 테이블]

| Table | Column   | Data Type | Length | Precision | Scale | Primary Key | Nullable                                                   | Default | Comment |
| ----- | -------- | --------- | ------ | --------- | ----- | ----------- | ---------------------------------------------------------- | ------- | ------- |
| EMP   | EMPNO    | NUMBER    | -      | 4         | 0     | 1           | -                                                          | -       | -       |
|       | ENAME    | VARCHAR2  | 10     | -         | -     | -           | ![nullable](http://127.0.0.1:8080/i/check_small_black.gif) | -       | -       |
|       | JOB      | VARCHAR2  | 9      | -         | -     | -           | ![nullable](http://127.0.0.1:8080/i/check_small_black.gif) | -       | -       |
|       | MGR      | NUMBER    | -      | 4         | 0     | -           | ![nullable](http://127.0.0.1:8080/i/check_small_black.gif) | -       | -       |
|       | HIREDATE | DATE      | 7      | -         | -     | -           | ![nullable](http://127.0.0.1:8080/i/check_small_black.gif) | -       | -       |
|       | SAL      | NUMBER    | -      | 7         | 2     | -           | ![nullable](http://127.0.0.1:8080/i/check_small_black.gif) | -       | -       |
|       | COMM     | NUMBER    | -      | 7         | 2     | -           | ![nullable](http://127.0.0.1:8080/i/check_small_black.gif) | -       | -       |
|       | DEPTNO   | NUMBER    | -      | 2         | 0     | -           | ![nullable](http://127.0.0.1:8080/i/check_small_black.gif) | -       | -       |



# INNER JOIN

## SELECT FROM에서의 조인

- DEPT, EMP 테이블 조인
- DEPTNO가 공통 컬럼
- 각 테이블의 DEPTNO를 이용해서 연결해준다.

```SQL
SELECT D.DEPTNO, E.EMPNO FROM DEPT D, EMP E
WHERE D.DEPTNO = E.DEPTNO;
```

| DEPTNO | EMPNO |
| ------ | ----- |
| 10     | 7839  |
| 30     | 7698  |
| 10     | 7782  |
| 20     | 7566  |
| 20     | 7788  |
| 20     | 7902  |
| 20     | 7369  |
| 30     | 7499  |
| 30     | 7521  |
| 30     | 7654  |
| 30     | 7844  |
| 20     | 7876  |
| 30     | 7900  |
| 10     | 7934  |





## JOIN을 이용한 명시적 조인 (ANSI 표준)

- 형태

```SQL
SELECT 컬럽1, 컬럼2, ... 
FROM 테이블1
JOIN 테이블2
ON 테이블1.컬렴 = 테이블2.컬럼;
```



```SQL
SELECT D.DEPTNO, E.EMPNO
FROM DEPT D
JOIN EMP E
ON D.DEPTNO = E.DEPTNO;
```



| DEPTNO | EMPNO |
| ------ | ----- |
| 10     | 7839  |
| 30     | 7698  |
| 10     | 7782  |
| 20     | 7566  |
| 20     | 7788  |
| 20     | 7902  |
| 20     | 7369  |
| 30     | 7499  |
| 30     | 7521  |
| 30     | 7654  |
| 30     | 7844  |
| 20     | 7876  |
| 30     | 7900  |
| 10     | 7934  |



# OUTER JOIN

- 여러 테이블 간에 공통된 컬럼으로 연결되는 내부조인과 다르게 어느 한 테이블에 다른 테이블과 같은 컬럼이 없더라도 결과들이 조회결과에 포함되게 하는 조인
- OUTER JOIN은 연산자 `(+)`를 사용한다.
- JOIN 시킬 때 보고 싶은 데이터가 있지만 데이터가 없을 수도 있는 쪽 컬럼에 (+)를 추가하여 외부 조인이 가능하다.



## 예

- EMP 테이블의 HIREDATE도 출력하고 싶을 때

```SQL
SELECT D.DEPTNO, E.EMPNO, E.HIREDATE
FROM DEPT D, EMP E
WHERE D.DEPTNO = E.DEPTNO (+);
```



### 결과

| DEPTNO | EMPNO | HIREDATE   |
| ------ | ----- | ---------- |
| 10     | 7839  | 11/17/1981 |
| 30     | 7698  | 05/01/1981 |
| 10     | 7782  | 06/09/1981 |
| 20     | 7566  | 04/02/1981 |
| 20     | 7788  | 12/09/1982 |
| 20     | 7902  | 12/03/1981 |
| 20     | 7369  | 12/17/1980 |
| 30     | 7499  | 02/20/1981 |
| 30     | 7521  | 02/22/1981 |
| 30     | 7654  | 09/28/1981 |
| 30     | 7844  | 09/08/1981 |
| 20     | 7876  | 01/12/1983 |
| 30     | 7900  | 12/03/1981 |
| 10     | 7934  | 01/23/1982 |
| 40     | -     | -          |



### (+)를 사용 안하고 했을 경우

- 마지막 HIREDATE, EMPNO가 NULL 인 경우의 ROW는 나오지 않는 것을 볼 수 있다.

```SQL
SELECT D.DEPTNO, E.EMPNO, E.HIREDATE
FROM DEPT D, EMP E
WHERE D.DEPTNO = E.DEPTNO;
```



### 결과

| DEPTNO | EMPNO | HIREDATE   |
| ------ | ----- | ---------- |
| 10     | 7839  | 11/17/1981 |
| 30     | 7698  | 05/01/1981 |
| 10     | 7782  | 06/09/1981 |
| 20     | 7566  | 04/02/1981 |
| 20     | 7788  | 12/09/1982 |
| 20     | 7902  | 12/03/1981 |
| 20     | 7369  | 12/17/1980 |
| 30     | 7499  | 02/20/1981 |
| 30     | 7521  | 02/22/1981 |
| 30     | 7654  | 09/28/1981 |
| 30     | 7844  | 09/08/1981 |
| 20     | 7876  | 01/12/1983 |
| 30     | 7900  | 12/03/1981 |
| 10     | 7934  | 01/23/1982 |



## OUTER JOIN 제약사항

- (+)는 컬럼에만 붙일 수 있으며, OR 연산자와 같이 사용 못한다.
- 외부조인시 서브쿼리와 같이 사용하지 못한다.
- (+)은 한쪽에만 붙일 수 있다.



## LEFT JOIN

- 왼쪽 테이블에만 있는 데이터를 모두 보고자 할 때

```SQL
SELECT D.DEPTNO, D.LOC, E.EMPNO
FROM DEPT D, EMP E
WHERE D.DEPTNO (+) = E.DEPTNO;
```



```SQL
SELECT D.DEPTNO, D.LOC, E.EMPNO
FROM DEPT D
LEFT OUTER JOIN EMP E
ON D.DEPTNO = E.DEPTNO;
```



## RIGHT JOIN

- 오른쪽 테이블에만 있는 데이터를 모두 보고자 할 때

```SQL
SELECT D.DEPTNO, E.EMPNO, E.HIREDATE
FROM DEPT D, EMP E
WHERE D.DEPTNO = E.DEPTNO (+);
```



```SQL
SELECT D.DEPTNO, E.EMPNO, E.HIREDATE
FROM DEPT D
RIGHT OUTER JOIN EMP E
ON D.DEPTNO = E.DEPTNO;
```





# CROSS JOIN

- Cartesian Product라고 하며 모든 경우의 수를 보여주는 조인.



### 예

```SQL
SELECT D.DEPTNO, E.EMPNO, E.NAME
FROM DEPT D, EMP E;
```

| DEPTNO | EMPNO | ENAME  |
| ------ | ----- | ------ |
| 10     | 7839  | KING   |
| 10     | 7698  | BLAKE  |
| 10     | 7782  | CLARK  |
| 10     | 7566  | JONES  |
| 10     | 7788  | SCOTT  |
| 10     | 7902  | FORD   |
| 10     | 7369  | SMITH  |
| 10     | 7499  | ALLEN  |
| 10     | 7521  | WARD   |
| 10     | 7654  | MARTIN |
| 10     | 7844  | TURNER |
| 10     | 7876  | ADAMS  |
| 10     | 7900  | JAMES  |
| 10     | 7934  | MILLER |
| 20     | 7839  | KING   |
| 20     | 7698  | BLAKE  |
| 20     | 7782  | CLARK  |
| 20     | 7566  | JONES  |
| 20     | 7788  | SCOTT  |
| 20     | 7902  | FORD   |
| 20     | 7369  | SMITH  |
| 20     | 7499  | ALLEN  |
| 20     | 7521  | WARD   |
| 20     | 7654  | MARTIN |
| 20     | 7844  | TURNER |
| 20     | 7876  | ADAMS  |
| 20     | 7900  | JAMES  |
| 20     | 7934  | MILLER |
| 30     | 7839  | KING   |
| 30     | 7698  | BLAKE  |
| 30     | 7782  | CLARK  |
| 30     | 7566  | JONES  |
| 30     | 7788  | SCOTT  |
| 30     | 7902  | FORD   |
| 30     | 7369  | SMITH  |
| 30     | 7499  | ALLEN  |
| 30     | 7521  | WARD   |
| 30     | 7654  | MARTIN |
| 30     | 7844  | TURNER |
| 30     | 7876  | ADAMS  |
| 30     | 7900  | JAMES  |
| 30     | 7934  | MILLER |
| 40     | 7839  | KING   |
| 40     | 7698  | BLAKE  |
| 40     | 7782  | CLARK  |
| 40     | 7566  | JONES  |
| 40     | 7788  | SCOTT  |
| 40     | 7902  | FORD   |
| 40     | 7369  | SMITH  |
| 40     | 7499  | ALLEN  |
| 40     | 7521  | WARD   |
| 40     | 7654  | MARTIN |
| 40     | 7844  | TURNER |
| 40     | 7876  | ADAMS  |
| 40     | 7900  | JAMES  |
| 40     | 7934  | MILLER |





# SELF JOIN

- 같은 테이블을 대상으로 조인을 사용한 것을 말하며 셀프 조인의 경우 테이블에 별명을 붙여서 사용한다.



# ANTI JOIN

- NOT IN 연산자를 사용하는 조인



# SEMI JOIN

- EXISTS 연산자를 사용하는 조인, 서브 쿼리내에서 존재하는 데이터만 추출
- ANTI JOIN의 반대
- SEMI JOIN의 결과값은 중복이 제거된다.



# References

- https://goddaehee.tistory.com/62
- https://hunit.tistory.com/225
- https://hunit.tistory.com/226?category=534447