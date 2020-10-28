---
layout: page
title: inner join과 outer join
tags: database
key: page-single
comment: true
comments: true
---
기본인데,, 당연히 알지^^ 자신했다 낭패 봐서 정리하는 글입니다,,흑,,   
 
 

## JOIN이란?
2개 이상의 테이블에 있는 정보 중 사용자가 필요한 집합에 맞게 가상의 테이블처럼 만들어서 결과를 보여주는 것이다.
 
  

## JOIN의 종류
<img class="image" src="https://www.techagilist.com/wp-content/uploads/2018/07/sql-joins.png"/>
그림만 보면 쉬운데,, 쿼리 결과에 대해서도 알아봅시다,,   
<br><br><br>
 


|----+----|
|종류|설명|
|----|----|
|INNER JOIN|특정 컬럼을 기준으로 정확히 매칭된 집합을 출력한다.|
|OUTER JOIN|특정 컬럼을 기준으로 매칭된 집합을 출력하지만 한쪽의 집합은 모두 출력하고 다른 한쪽의 집합은 매칭되는 컬럼의 값만을 출력한다.|
|SELF JOIN|동일한 테이블 끼리의 특정 컬럼을 기준으로 매칭되는 집합을 출력한다.|
|FULL OUTER JOIN|INNER, LEFT OUTER, RIGHT OUTER 조인 집합을 모두 출력한다.|
|CROSS JOIN|Cartesian Product라고도 하며 조인되는 두 테이블에서 곱집합을 반환한다.|
|NATURAL JOIN|특정 테이블의 같은 이름을 가진 컬럼 간의 조인집합을 출력한다.|
|----+----|
 
 
이들 중 **INNER JOIN** 과 **OUTER JOIN**에 대해서 알아봅시다!
 

## 예시 테이블
|----+----+----+----|
|TABLE_A||TABLE_B||
|----|----|----|----|
|id|fruit|id|fruit|
|1|Apple|1|Orange|
|2|Orange|2|Banana|
|3|Watermelon|3|Apple|
|----+----+----+----|
 
 
 

## INNER JOIN
특정 컬럼을 기준으로 정확히 매칭된 집합을 출력한다.
```
SELECT A.id, A.fruit, B.id , B.fruit
FROM TABLE_A A INNER JOIN TABLE_B B
ON A.fruit = B.fruit;
```
### 결과
|---+---+---+---|
|A.id|A.fruit|B.id|B.fruit|
|---|---|---|---|
|1|Apple|3|Apple|
|2|Orange|1|Orange|
|---+---+---+---|

## OUTER JOIN
특정 컬럼을 기준으로 매칭된 집합을 출력하지만 한쪽의 집합은 모두 출력하고 다른 한쪽의 집합은 매칭되는 컬럼의 값만을 출력한다.

### LEFT OUTER JOIN
```
SELECT A.id, A.fruit, B.id , B.fruit
FROM TABLE_A A LEFT JOIN TABLE_B B
ON A.fruit = B.fruit;
```
### 결과
|---+---+---+---|
|A.id|A.fruit|B.id|B.fruit|
|---|---|---|---|
|1|Apple|3|Apple|
|2|Orange|1|Orange|
|3|Watermelon|null|null|
|---+---+---+---|

### RIGHT OUTER JOIN
```
SELECT A.id, A.fruit, B.id , B.fruit
FROM TABLE_A A RIGHT JOIN TABLE_B B
ON A.fruit = B.fruit;
```
### 결과
|---+---+---+---|
|A.id|A.fruit|B.id|B.fruit|
|---|---|---|---|
|2|Orange|1|Orange|
|null|null|2|Banana|
|1|Apple|3|Apple|
|---+---+---+---|

### FULL OUTER JOIN
INNER, LEFT OUTER, RIGHT OUTER 조인 집합을 모두 출력하는 조인 방식이다. 즉, 두 테이블간 출력 가능한 모든 데이터를 포함한 집합을 출력한다.
```
SELECT A.id, A.fruit, B.id , B.fruit
FROM TABLE_A A FULL OUTER JOIN TABLE_B B
ON A.fruit = B.fruit;
```
|---+---+---+---+---|
|A.id|A.fruit|B.id|B.fruit|비고|
|---|---|---|---|---|
|1|Apple|3|Apple|INNER JOIN|
|2|Orange|1|Orange|INNER JOIN|
|3|Watermelon|null|null|LEFT OUTER JOIN|
|null|null|2|Banana|RIGHT OUTER JOIN|
|---+---+---+---+---|
