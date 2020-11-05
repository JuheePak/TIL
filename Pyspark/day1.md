### day 1: RDD

#### `RDD(Resilient Distributed Dataset)`

##### read-only 데이터셋으로서 다양한 머신에 데이터셋의 멀티셋(중복을 허용)을 분산해두고 특정한 머신에 문제가 생기더라도 문제없이 읽을수로 있도록 지원한다

- MapReduce 작업
- 분산하여 병렬적 처리
- 빠른 연산
- 불변(Immutable)
- Transformation 과 Action 으로 함수 종류가 나눠지며, Action 함수가 실행됐을 때 실제 연산
- Lineage(계보, '기록'정도로 이해하면 편할듯) 를 통해 Fault Tolerant(고장 내성) 보장



### `1. SparkSession 객체 생성`

``` python
import pyspark
from pyspark.sql import SparkSession
spark = SparkSession.builder.master("local[2]") \
                    .appName('') \ # 삭제 
                    .getOrCreate()
spark
```



### `2. 리스트객체로 RDD 객체 생성하기`

``` python
dataList = [("Java", 20000), ("Python", 100000), ("Scala", 3000)]
rdd=spark.sparkContext.parallelize(dataList)
print(rdd)
print(type(rdd))
print(rdd.collect())
```

``` python
import numpy as np
lst=np.random.randint(0,10,20)
rdd=spark.sparkContext.parallelize(lst)
print(type(rdd))
print(rdd.collect())
print(rdd.count())
```



### `3. 텍스트 파일 내용 읽어서 RDD 객체 생성하기`

``` python
rdd = spark.sparkContext.textFile(".txt") # 파일 이름 삭제
print(rdd.collect())
```



### `4. 생성한 RDD 객체 Spark Dataframe으로 변환하기`

``` python
dept = [("Finance",10), 
        ("Marketing",20), 
        ("Sales",30), 
        ("IT",40) 
      ]
rdd = spark.sparkContext.parallelize(dept)
print(rdd.collect())

df = rdd.toDF()
df.printSchema()
df.show()

deptColumns = ["dept_name","dept_id"]
df2 = rdd.toDF(deptColumns)
df2.printSchema()
df2.show(truncate=False)
```

``` python
data = [('James','','Smith','1991-04-01','M',3000),
  ('Michael','Rose','','2000-05-19','M',4000),
  ('Robert','','Williams','1978-09-05','M',4000),
  ('Maria','Anne','Jones','1967-12-01','F',4000),
  ('Jen','Mary','Brown','1980-02-17','F',-1)
]

columns = ["firstname","middlename","lastname","dob","gender","salary"]
df = spark.createDataFrame(data=data, schema = columns)
print(type(df))
print(df)
df.printSchema()
df.show()
```

