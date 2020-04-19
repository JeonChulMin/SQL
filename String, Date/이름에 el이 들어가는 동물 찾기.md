# 이름에 el이 들어가는 동물 찾기

## 문제 설명

`ANIMAL_INS` 테이블은 동물 보호소에 들어온 동물의 정보를 담은 테이블입니다. `ANIMAL_INS` 테이블 구조는 다음과 같으며, `ANIMAL_ID`, `ANIMAL_TYPE`, `DATETIME`, `INTAKE_CONDITION`, `NAME`, `SEX_UPON_INTAKE`는 각각 동물의 아이디, 생물 종, 보호 시작일, 보호 시작 시 상태, 이름, 성별 및 중성화 여부를 나타냅니다.

| NAME             | TYPE       | NULLABLE |
| ---------------- | ---------- | -------- |
| ANIMAL_ID        | VARCHAR(N) | FALSE    |
| ANIMAL_TYPE      | VARCHAR(N) | FALSE    |
| DATETIME         | DATETIME   | FALSE    |
| INTAKE_CONDITION | VARCHAR(N) | FALSE    |
| NAME             | VARCHAR(N) | TRUE     |
| SEX_UPON_INTAKE  | VARCHAR(N) | FALSE    |

보호소에 돌아가신 할머니가 기르던 개를 찾는 사람이 찾아왔습니다. 이 사람이 말하길 할머니가 기르던 개는 이름에 'el'이 들어간다고 합니다. 동물 보호소에 들어온 동물 이름 중, 이름에 EL이 들어가는 개의 아이디와 이름을 조회하는 SQL문을 작성해주세요. 이때 결과는 이름 순으로 조회해주세요. 단, 이름의 대소문자는 구분하지 않습니다.

## 예시

예를 들어 `ANIMAL_INS` 테이블이 다음과 같다면

| ANIMAL_ID | ANIMAL_TYPE | DATETIME            | INTAKE_CONDITION | NAME         | SEX_UPON_INTAKE |
| --------- | ----------- | ------------------- | ---------------- | ------------ | --------------- |
| A355753   | Dog         | 2015-09-10 13:14:00 | Normal           | Elijah       | Neutered Male   |
| A352872   | Dog         | 2015-07-09 17:51:00 | Aged             | Peanutbutter | Neutered Male   |
| A353259   | Dog         | 2016-05-08 12:57:00 | Injured          | Bj           | Neutered Male   |
| A373219   | Cat         | 2014-07-29 11:43:00 | Normal           | Ella         | Spayed Female   |
| A382192   | Dog         | 2015-03-13 13:14:00 | Normal           | Maxwell 2    | Intact Male     |

- 이름에 'el'이 들어가는 동물은 Elijah, Ella, Maxwell 2입니다.
- 이 중, 개는 Elijah, Maxwell 2입니다.

따라서 SQL문을 실행하면 다음과 같이 나와야 합니다.

| ANIMAL_ID | NAME      |
| --------- | --------- |
| A355753   | Elijah    |
| A382192   | Maxwell 2 |



## 정답

```sql
-- 코드를 입력하세요
SELECT ANIMAL_ID, NAME FROM ANIMAL_INS
WHERE  ANIMAL_TYPE = 'Dog' AND (NAME LIKE 'El%' OR NAME LIKE '%el%') 
ORDER BY NAME ASC
```

- `%`는 앞, 뒤, 중간 어디나 올 수 있으며 조건식을 검색할 때 대소문자를 구분!



```sql
-- 코드를 입력하세요
SELECT ANIMAL_ID, NAME FROM ANIMAL_INS
WHERE  ANIMAL_TYPE = 'Dog' AND REGEXP_LIKE(NAME, 'El|el', 'i') 
ORDER BY NAME ASC
```

- LIKE 문을 IN을 사용하듯이 사용하고 싶을 경우, 조건이 여러 개인 경우
- 오라클 10g이상부터 REGEXP_LIKE를 사용 가능
- `|` 를 사용해서 LIKE 조건을 걸 단어를 구분한다.
- 세 번째 인자로 `'i'`  를 주면 대, 소문자 구분을 하지 않는다.





Reference

- https://dpdpwl.tistory.com/117