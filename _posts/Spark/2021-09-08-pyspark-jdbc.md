---
title: Pyspark
excerpt: Pyspark SQL 기초 정리

categories:
  - Spark

tags:
  - Spark
  - pyspark
  - pysparkSQL
  - Python

toc: true
toc_sticky: true
toc_label: Index
---

# 1. pyspark 사용하기 위한 준비
---
## 1) Import library
```python
from pyspark.sql import SparkSession
from pyspark.sql.functions import count, desc, col, max
```

## 2) Create Session
```python
# Spark web UI에 노출될 appName 생성
spark = SparkSession.builder.appName('spark_app').getOrCreate()
```


## 3) Read CSV
```python
csv_path = '~/<path>/csv_file_name.csv'
df = spark.read.format('csv').option('inferSchema',True).option('header',True).load(csv_path)
```

- `spark` : Session
- `read.format('csv')` : 파일 format 선언
- `option('inferSchema',boolean)` : `True`일 경우 Column Type 지정 , False 일 경우 지정 X
- `option('header',True)` : 헤더의 여부
- `load(path)` : 파일 경로 


# 2. DataFrame 다루기
---
## 1) 데이터 확인
### (1) DataFrame 확인
```python
df.show()
```

### (2) Schema 확인
```python
df.printSchema()
```

### (3) DataFrame Shape
```python
shape = (df.count(), len(df.columns))
```

## 2) Row, Columns
### (1) Drop Column
```python
df = df.drop('Column_name')
```

### (2) Column Name
```python
df.columns
```

### (3) length of columns
```python
len(df.columns)
```

### (4) length of rows
```python
df.count()
```

## 3) NA Handling
````python
df = df.na.drop()
````

# 3. Query
## 1) SELECT
````python
q0 = df.select('col_1', 'col_2')
q0.show()
````

## 2) 특정 조건 필터링 (like Where)
- filter 사용
| customer 컬럼이 DDory 인 경우
````python
q1 = df.select('*').filter(df.customer == 'DDory')
q1.show()
````
- SQL의 경우
```sql
SELECT *
FROM <table>
WHERE customer = 'DDory';
```

### Ex 1) top 10 users who are fan of Rihanna
- Pyspark
```python
ex1 = df.select('user_id').filter(df.artist == 'Rihanna')\
    .groupby('user_id').agg(count('user_id').alias('count'))\
    .orderBy(desc('count')).limit(10)
```

- SQL(Postgresql)
```sql
SELECT user_id, count(*) as count
FROM <table>
WHERE artist = 'Rihanna'
GROUP BY user_id
ORDER BY count(*) desc
LIMIT 10;
```

### Ex 2) Find top 10 famous tracks
- Pyspark
````python
ex2 = df.select('artist', 'track').groupby('artist','track')\
    .agg(count('*').alias('count')).orderBy(desc('count')).limit(10)
````

- SQL(Postgresql)
```sql
SELECT artist, track, count(*) as count
FROM <table>
GROUP BY artist, track
ORDER BY count(*) desc
LIMIT 10;
```
### Ex 3) Find top 10 famous tracks of Rihanna
```python
ex3 = df.select('artist','track').filter(listening_df.artist == 'Rihanna')\
    .groupby('artist','track').agg(count('*').alias('count')).orderBy(desc('count')).limit(10)
```

### Ex 4) Find top 10 famous albums
```python
ex4 = df.select('artist','album').groupby('artist','album')\
    .agg(count('*').alias('count')).orderBy(desc('count')).limit(10)
```