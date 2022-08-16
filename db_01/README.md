# 사전 설정

## 실행

```bash
$ sqlite3 healthcare.sqlite3 
```

## Column 출력 설정

```sql
sqlite3> .headers on 
sqlite3> .mode column
```

## table 및 스키마 조회

```sql
sqlite3> .tables
healthcare

sqlite3> .schema healthcare
CREATE TABLE healthcare (
id PRIMARY KEY,        
sido INTEGER NOT NULL, 
gender INTEGER NOT NULL,
age INTEGER NOT NULL,  
height INTEGER NOT NULL,
weight INTEGER NOT NULL,
waist REAL NOT NULL,   
va_left REAL NOT NULL, 
va_right REAL NOT NULL,

blood_pressure INTEGER 
NOT NULL,
smoking INTEGER NOT NULL,
is_drinking BOOLEAN NOT NULL
);
```

# 문제

### 1. 추가되어 있는 모든 데이터의 수를 출력하시오.

```sql
SELECT COUNT(*) FROM healthcare;
-- : 주석기능
```

```
COUNT(*)
--------
1000000
```

### 2. 나이 그룹이 10(age)미만인 사람의 수를 출력하시오.

```sql
select count(*) from healthcare where age < 10
```

```
count(*)
--------
156277
```

### 3. 성별이 1인 사람의 수를 출력하시오.

```sql
select count(*) from healthcare where gender = 1 --'=='이 아니라 '='를 사용
```

```
count(*)
--------
510689
```

### 4. 흡연 수치(smoking)가 3이면서 음주(is_drinking)가 1인 사람의 수를 출력하시오.

```sql
select count(*) from healthcare where is_drinking = 1 and smoking = 3 ; --and 사용가능한듯
```

```
count(*)
--------
150361
```

### 5. 양쪽 시력이(va_left, va_right) 모두 2.0이상인 사람의 수를 출력하시오.

```sql
select count(*) from healthcare where va_left >= 2.0 and va_right >= 2.0 ;
```

```
count(*)
--------
2614
```

### 6. 시도(sido)를 모두 중복 없이 출력하시오.

```sql
select distinct sido from healthcare ; 
--select distinct *원하는열 : 중복행제거하고 출력해줌
```

```
sido
----
36
27
11
31
41
44
48
30
42
43
46
28
26
47
45
29
49
```

### 허리 둘레가 75이상이면서 몸무게가 60이하인 사람.

```sql
select count(*) from healthcare where waist >= 75 and weight <= 60 ;
```

```
count(*)
--------
310768
```

### 허리 둘레가 75이상이거나 몸무게가 60이하인 사람.

```sql
select count(*) from healthcare where waist >= 75 or weight <= 60 ;
```

```
count(*)
--------
993242
```

### 허리 둘레가 75이상이이면서 몸무게가 60이하이면서 흡연하지 않는 사람.

```sql
select count(*) from healthcare where waist >= 75 and weight <= 60 and smoking = 0;
--흡연자 칸에 0은 없고 1,2,3값만 있네
```

```
count(*)
--------
0
```

### 허리 둘레가 75이상이이면서 몸무게가 60이하이면서 sido가 11 이 아닌사람.

```sql
select count(*) from healthcare where waist >= 75 and weight <= 60 and not sido = 11;
-- and not 과 != 사용 가능
```

```
count(*)
--------
257429
```

### 비만도를 측정하여 비만인 인원수 구하기(BMI지수가 25이상부터 비만).

```sql
select count(*) from healthcare where weight*10000/(height*height) >= 25;
-- 연산이 가능하다
```

```
count(*)
--------
366893
```