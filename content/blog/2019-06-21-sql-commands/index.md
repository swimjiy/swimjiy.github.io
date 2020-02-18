---
slug: 2019-06-21-sql-commands
title:        "[etc] SQL 명령문 정리"
description:     "정보처리기사 실기 2과목의 SQL문 정리"
date:         2019-06-21
published: true
banner: './etc.jpg'
categories: [etc]
tags:
    - SQL
---



정보처리기사 실기를 공부하면서 2과목 데이터베이스에 나오는 SQL문을 간략하게 정리했다.

**예시 코드의 대괄호`[]` 는 생략이 가능하다는 표시!**

<br/>

## DDL

DDL(Data Definition Language)은 스키마, 도메인, 테이블, 뷰, 인덱스를 정의하거나 변경 또는 제거할 때 사용하는 언어이다.



#### CREATE SCHEMA

```sql
CREATE SCHEMA 스키마명 AUTHORIZATION 사용자_ID;
```



#### CREATE DOMAIN

```sql
CREATE DOMAIN 도메인명 데이터_타입
[DEFAULT 기본값]
[CONSTRAINT 제약조건명 CHECK (범위 값)];
```



#### CREATE TABLE

```sql
CREATE TABLE 테이블명
	(속성명 데이터_타입 [NOT NULL],
 	[,PRIMARY KEY(기본키_속성명)]
    [,UNIQUE(대체키_속성명)]
    [,FOREIGN KEY(외래키_속성명)
    	REFERENCES 참조테이블(기본키_속성명)]
     	[ON DELETE 옵션]
     	[ON UPDATE 옵션]
    [,CONSTRAINT 제약조건명][CHECK(조건식)];
	
);
```



#### CREATE VIEW

```sql
CREATE VIEW 뷰명[(속성명)]
	AS SELECT문;
```



#### CREATE INDEX

```sql
CREATE [UNIQUE] INDEX 인덱스명
	ON 테이블명(속성명 [ASC | DESC])
	[CLUSTER];
```



#### CREATE TRIGGER

```sql
CREATE TRIGGER 트리거명 [동작시기 옵션][동작 옵션] ON 테이블명
REFERENCING [NEW | OLD] TABLE AS 테이블명
FOR EACH ROW
WHEN 조건식
BEGIN
	트리거 본문 코드
END;
```



#### ALTER TABLE

```sql
ALTER TABLE 테이블명 ADD 속성명 데이터_타입 [DEFAULT '기본값'];
ALTER TABLE 테이블명 ALTER 속성명 데이터_타입 [SET DEFAULT '기본값'];
ALTER TABLE 테이블명 DROP COLUMN 속성명 [CASCADE];
```



#### DROP

```sql
DROP SCHEMA 스키마명 [CASCADE | RESTRICT];
DROP DOMAIN 도메인명 [CASCADE | RESTRICT];
DROP TABLE 테이블명 [CASCADE | RESTRICT];
DROP VIEW 뷰명 [CASCADE | RESTRICT];
DROP INDEX 인덱스명 [CASCADE | RESTRICT];
DROP TRIGGER 트리거명 [CASCADE | RESTRICT];
DROP CONSTRAINT 제약조건명;
```



<br/>

## SELECT

SELECT문은 테이블을 구성하는 튜플들 중에서 전체 또는 조건을 만족하는 튜플을 검색하여 주기억장치에 임시 테이블로 구성하는 명령문이다.

```sql
SELECT [DISTINCT][테이블명.]속성명[AS 별칭]
FROM 테이블명
[WHERE 조건]
[GROUP BY 속성명]
[HAVING 조건]
[ORDER BY 속성명 [ASC | DESC]];
```



#### 참고 함수

```
COUNT(속성명) : 그룹별 튜플 수
MAX(속성명) : 그룹별 최대값
MIN(속성명) : 그룹별 최소값
SUM(속성명) : 그룹별 합계
AVG(속성명) : 그룹별 평균
Trim(속성명) : 좌우 공백 제거
Left([속성명],숫자) : 왼쪽으로 숫자만큼만 선택 
Right([속성명],숫자) : 오른쪽으로 숫자만큼만 선택
Month([속성명]) : 속성명의 '월'만 추출
```



<br/>

## JOIN

JOIN은 2개의 테이블에 대해 연관된 튜플들을 결합하여 하나의 새로운 릴레이션을 반환한다.



#### INNER JOIN

```sql
/*WHERE절을 이용한 EQUL JOIN*/
SELECT [테이블명1.]속성명, [테이블명2.]속성명
FROM 테이블명1, 테이블명2
WHERE 테이블명1.속성 = 테이블명2.속성;

/*NATURAL JOIN을 이용한 EQUL JOIN*/
SELECT [테이블명1.]속성명, [테이블명2.]속성명
FROM 테이블명1 NATURAL JOIN 테이블명2;

/*JOIN~USING절을 이용한 EQUL JOIN*/
SELECT [테이블명1.]속성명, [테이블명2.]속성명
FROM 테이블명1 JOIN 테이블명2 USING(속성명);
```



#### OUTER JOIN

```sql
/*LEFT OUTER JOIN 방법1*/
SELECT [테이블명1.]속성명, [테이블명2.]속성명
FROM 테이블명1 LEFT OUTER JOIN 테이블명2
ON 테이블명1.속성명 = 테이블명2.속성명;

/*LEFT OUTER JOIN 방법2*/
SELECT [테이블명1.]속성명, [테이블명2.]속성명
FROM 테이블명1, 테이블명2
WHERE 테이블명1.속성명 = 테이블명2.속성명(+);

/*RIGHT OUTER JOIN 방법1*/
SELECT [테이블명1.]속성명, [테이블명2.]속성명
FROM 테이블명1 LEFT OUTER JOIN 테이블명2
ON 테이블명1.속성명 = 테이블명2.속성명;

/*RIGHT OUTER JOIN 방법2*/
SELECT [테이블명1.]속성명, [테이블명2.]속성명
FROM 테이블명1, 테이블명2
WHERE 테이블명1.속성명(+) = 테이블명2.속성명;

/*FULL OUTER JOIN*/
SELECT [테이블명1.]속성명, [테이블명2.]속성명
FROM 테이블명1 FULL OUTER JOIN 테이블명2
ON 테이블명1.속성명 = 테이블명2.속성명;
```

<br/>

## DML

DML(Data Manipulation Language)은 DB사용자가 응용 프로그램이나 질의어를 통해 저장된 데이터를 실질적으로 관리하는 데 사용하는 언어이다.



#### INSERT

```sql
INSERT INTO 테이블명
VALUES (데이터1, 데이터2 ...);
```



#### DELETE

```sql
DELETE FROM 테이블명
WHERE 조건;
```



#### UPDATE

```sql
UPDATE 테이블명
SET 속성명=데이터
WHERE 조건;
```

<br/>

## DCL

DCL(Data Control Language)은 데이터의 보안, 무결성, 회복, 병행 제어 등을 정의하는 데 사용하는 언어이다.



#### GRANT

```sql
GRANT 권한_리스트 ON 개체 TO 사용자 [WITH GRANT OPTION]; 
```



#### REVOKE

```sql
REVOKE [GRANT OPTION FOR] 권한_리스트 ON 개체 FROM 사용자 [CASCADE];
```



<br/>

## Refer

[2019 시나공 정보처리기사 실기 - 길벗](<https://www.gilbut.co.kr/book/view?bookcode=BN002360>)