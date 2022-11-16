
문서정보 : 2022.11.16. 작성, 작성자 [@SAgiKPJH](https://github.com/SAgiKPJH)

<br>

# PostgreSQL로 시작하는 SQL 코딩 입문
SQL Programming in PostgreSQL



### 목표

- [ ] 1장. SQL 활용력을 높이자
  - [ ] 1.1 조회 결과의 가공
    - [ ] 1.1.1 검색 결과 정렬하기
    - [ ] 1.1.2 검색 결과 제한하기
    - [ ] 1.1.3 함수를 이용한 행 단위 연산
    - [ ] 1.1.4 VALUES 목록
  - [ ] 1.2 데이터 그룹화
    - [ ] 1.2.1 GROUP BY
    - [ ] 1.2.2 HAVING
  - [ ] 1.3 집계 함수(Aggregate Functions)의 사용
    - [ ] 1.3.1 COUNT 함수
    - [ ] 1.3.2 SUM 함수
    - [ ] 1.3.3 AVG 함수
    - [ ] 1.3.4 MIN 함수
    - [ ] 1.3.5 MAX 함수
    - [ ] 1.3.6 DISTINCT 함수
  - [ ] 1.4 서브 쿼리(SUB-QUERY)
    - [ ] 1.4.1 서브 쿼리(SUB-QUERY)란?
    - [ ] 1.4.2 단일행 서브 쿼리
    - [ ] 1.4.3 다중행 서브 쿼리
    - [ ] 1.4.4 다중 컬럼 서브 쿼리
    - [ ] 1.4.5 상관 서브 쿼리
    - [ ] 1.4.6 스칼라 서브 쿼리
    - [ ] 1.4.7 WITH 서브 쿼리(공통 테이블 표현식)
    - [ ] 1.4.8 인라인 뷰(INLINE VIEW)와 추출 테이블(DERIVED TABLE)
  - [ ] 1.5 집합 연산
  - [ ] 1.6 데이터의 계층적 질의
- [ ] 2장. 도전! SQL 레벨업
  - [ ] 2.1 다중 행의 결과를 하나의 행에 나열
    - [ ] 2.1.1 컬럼 값 연결(COLUMN VALUES CONCATENATION)
    - [ ] 2.1.2 행을 열로 바꾸는 방법, 피봇(PIVOT)
  - [ ] 2.2 단일 행을 다중 행으로 변환
    - [ ] 2.2.1 하나의 열에 나열된 문자열을 다중 행으로 변환
    - [ ] 2.2.2 단일 행의 다중 열을 다중 행으로 변환, 언피봇(UNPIVOT)
  - [ ] 2.3 그룹 함수를 이용한 소계, 총계 구하기
    - [ ] 2.3.1 ROLLUP
    - [ ] 2.3.2 CUBE
    - [ ] 2.3.3 GROUPING SETS
  - [ ] 2.4 윈도우 함수에 대한 이해와 활용
  - [ ] 2.5 페이지 처리
  - [ ] 2.6 복잡한 DML 문장
    - [ ] 2.6.1 SELECT 구문을 활용한 INSERT
    - [ ] 2.6.2 SELECT 구문을 활용한 UPDATE, DELETE
    - [ ] 2.6.3 JOIN을 통한 UPDATE
    - [ ] 2.6.4 JOIN을 통한 단일 테이블 DELETE
    - [ ] 2.6.5 다중 테이블 INSERT
    - [ ] 2.6.6 다중 테이블 UPDATE
    - [ ] 2.6.7 다중 테이블 DELETE
    - [ ] 2.6.8 다양한 DML을 한 번에 처리
    - [ ] 2.6.9 데이터 유무에 따른 UPDATE, INSERT 분기 처리

### 제작자
[@SAgiKPJH](https://github.com/SAgiKPJH)

### 참조

- [PostgreSQL로 시작하는 SQL 코딩입문 Part 02 활용편](http://www.yes24.com/Product/Goods/87579609)

---

<br><br>

# 1장. SQL 활용력을 높이자

기본적인 SQL 문장의 구성과 사용 방법을 통해, SQL 활용 능력을 배가 시키기 위한 다양한 SQL 문장 구성과 활용 사례를 설명한다.  
또한 실무에서 접할 수 있는 다양한 상황을 가정하여 SQL로 해결하는 방법도 살펴보자.

<br><br> 

## 1.1 조회 결과의 가공

테이블에 저장된 데이터를 원하는 조건으로 검색하여 조회하는 방법, 검색 조건을 지정하는 방법, 집합을 연결하는 방법등 기본적인 SELECT 문장의 사용 방법을 통해 **임의의 테이블 또는 여러 테이블을 연결하여 데이터를 조회할 때 실행 결과를 원하는 형태로 재구성하거나 가공하여 조회하는 방법에 대해 설명한다.  
또한 가독성, 결과값을 만들어 내기 위해, IF ~ Then ~ ElSE 와 같은 제어문 SELECT 문장에서 사용하는 방법등 다양한 활용방법도 다룬다.

<br>

### 1.1.1 검색 결과 정렬하기

대부분의 DBMS는 저장된 데이터를 조회할 때 조회 입력(INSERT)순서로 행들이 출력된다.  
원하는 기준에 따른 순서를 출력하기 위해 ORDER BY절을 사용하는데, SELECT 문장의 마지막 위치에 ORDER BY절을 추가함으로써 FROM과 WHERE 절에 의해 만들어진 검색 결과 집합에 대해 SELECT 절에 기술된 내용에 다따라 가공 처리된 결과 값을 ORDER BY절에 지정된 순서에 따라 정렬하여 출력한다.
```postgresql
SELECT 컬럼1, 컬럼2, ...
FROM 테이블1
WHERE 검색조건
ORDER BY 정렬기준컬럼1(첫번째_정렬기준) ASC,
         정렬기준컬럼2(두번째_정렬기준) DESC;
```

[책갈피-GitHub등록-<br>개수수정]

<br> 

### 1.1.2 검색 결과 제한하기

<br><br><br> 

### 1.1.3 함수를 이용한 행 단위 연산

<br><br><br> 

### 1.1.4 VALUES 목록

<br><br> 

## 1.2 데이터 그룹화

<br><br><br> 

### 1.2.1 GROUP BY

<br><br><br> 

### 1.2.2 HAVING

<br><br> 

## 1.3 집계 함수(Aggregate Functions)의 사용

<br><br><br> 

### 1.3.1 COUNT 함수

<br><br><br> 

### 1.3.2 SUM 함수

<br><br><br> 

### 1.3.3 AVG 함수

<br><br><br> 

### 1.3.4 MIN 함수

<br><br><br> 

### 1.3.5 MAX 함수

<br><br><br> 

### 1.3.6 DISTINCT 함수

<br><br> 

## 1.4 서브 쿼리(SUB-QUERY)

<br><br><br> 

### 1.4.1 서브 쿼리(SUB-QUERY)란?

<br><br><br> 

### 1.4.2 단일행 서브 쿼리

<br><br><br> 

### 1.4.3 다중행 서브 쿼리

<br><br><br> 

### 1.4.4 다중 컬럼 서브 쿼리

<br><br><br> 

### 1.4.5 상관 서브 쿼리

<br><br><br> 

### 1.4.6 스칼라 서브 쿼리

<br><br><br> 

### 1.4.7 WITH 서브 쿼리(공통 테이블 표현식)

<br><br><br> 

### 1.4.8 인라인 뷰(INLINE VIEW)와 추출 테이블(DERIVED TABLE)

<br><br> 

## 1.5 집합 연산

<br><br> 

## 1.6 데이터의 계층적 질의

<br> 

# 2장. 도전! SQL 레벨업

<br><br> 

## 2.1 다중 행의 결과를 하나의 행에 나열

<br><br><br> 

### 2.1.1 컬럼 값 연결(COLUMN VALUES CONCATENATION)

<br><br><br> 

### 2.1.2 행을 열로 바꾸는 방법, 피봇(PIVOT)

<br><br> 

## 2.2 단일 행을 다중 행으로 변환

<br><br><br> 

### 2.2.1 하나의 열에 나열된 문자열을 다중 행으로 변환

<br><br><br> 

### 2.2.2 단일 행의 다중 열을 다중 행으로 변환, 언피봇(UNPIVOT)

<br><br> 

## 2.3 그룹 함수를 이용한 소계, 총계 구하기

<br><br><br> 

### 2.3.1 ROLLUP

<br><br><br> 

### 2.3.2 CUBE

<br><br><br> 

### 2.3.3 GROUPING SETS

<br><br> 

## 2.4 윈도우 함수에 대한 이해와 활용

<br><br> 

## 2.5 페이지 처리

<br><br> 

## 2.6 복잡한 DML 문장

<br><br><br> 

### 2.6.1 SELECT 구문을 활용한 INSERT

<br><br><br> 

### 2.6.2 SELECT 구문을 활용한 UPDATE, DELETE

<br><br><br> 

### 2.6.3 JOIN을 통한 UPDATE

<br><br><br> 

### 2.6.4 JOIN을 통한 단일 테이블 DELETE

<br><br><br> 

### 2.6.5 다중 테이블 INSERT

<br><br><br> 

### 2.6.6 다중 테이블 UPDATE

<br><br><br> 

### 2.6.7 다중 테이블 DELETE

<br><br><br> 

### 2.6.8 다양한 DML을 한 번에 처리

<br><br><br> 

### 2.6.9 데이터 유무에 따른 UPDATE, INSERT 분기 처리





