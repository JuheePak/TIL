### day 2: Spark DataFrame



### `Spark DataFrame`

- DataFrame은 명명 된 열로 구성된 데이터 세트 
- 개념적으로는 관계형 데이터베이스의 테이블 또는 R / Python의 데이터 프레임과 동일하지만 내부적으로 더욱  최적화가 있음
- RDB Table처럼 Schema를 가지고 있고 RDB의 Table 연산이 가능
- 구조화 된 데이터 파일, Hive의 테이블, 외부 데이터베이스 또는 기존 RDD와 같은 다양한 소스 에서 구성 할 수 있늠 
- DataFrame API는 Scala, Java, Python 및 R 에서 사용할 수 있음
- SparkSQL을 통해 사용 가능



``` python
dept = [("Finance",10), 
        ("Marketing",20), 
        ("Sales",30), 
        ("IT",40) 
      ]
rdd = spark.sparkContext.parallelize(dept)
print(rdd.collect())
```

![캡처](https://user-images.githubusercontent.com/69948723/98310075-771e3a00-200f-11eb-91e4-a8c573b259b6.JPG)



### `생성한 RDD 객체 DataFrame으로 변환하기`

``` python
df = rdd.toDF() # 데이터 프레임으로 변환
df.printSchema()
df.show()
```

![캡처1](https://user-images.githubusercontent.com/69948723/98310080-784f6700-200f-11eb-9cb5-6f0aa0088d59.JPG)

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

![캡처2](https://user-images.githubusercontent.com/69948723/98310196-b482c780-200f-11eb-96e6-f727182d09e4.JPG)

``` python
from pyspark.sql.types import StructType,StructField, StringType, IntegerType
data2 = [("James","","Smith","36636","M",3000),
    ("Michael","Rose","","40288","M",4000),
    ("Robert","","Williams","42114","M",4000),
    ("Maria","Anne","Jones","39192","F",4000),
    ("Jen","Mary","Brown","","F",-1)
  ]

schema = StructType([ \
    StructField("firstname",StringType(),True), \
    StructField("middlename",StringType(),True), \
    StructField("lastname",StringType(),True), \
    StructField("id", StringType(), True), \
    StructField("gender", StringType(), True), \
    StructField("salary", IntegerType(), True) \
  ])
 
df = spark.createDataFrame(data=data2,schema=schema)
df.printSchema()
df.show(truncate=False)
```

![캡처4](https://user-images.githubusercontent.com/69948723/98310251-ce240f00-200f-11eb-9967-62570cc67da6.JPG)



csv, json 파일은 파이썬과 동일하게 import 하면 된다.

parquet 파일은 처음이니까 이것만 수행해본다.

### `Parquet 파일 내용 읽어서 DataFrame 객체 생성하기`

``` python
df = spark.read.load("data/userdata1.parquet")
df = df.select("first_name", "last_name", "email")
df.show()
```

![캡처5](https://user-images.githubusercontent.com/69948723/98310374-15aa9b00-2010-11eb-8b39-46ab164448da.JPG)



### `직접 DataFrame 객체 생성하여 정보 출력하기`

``` python
data = [("James","","Smith","36636","M",60000),
        ("Michael","Rose","","40288","M",70000),
        ("Robert","","Williams","42114","",400000),
        ("Maria","Anne","Jones","39192","F",500000),
        ("Jen","Mary","Brown","","F",0)]

columns = ["first_name","middle_name","last_name","dob","gender","salary"]
pysparkDF = spark.createDataFrame(data = data, schema = columns)
pysparkDF.printSchema()
pysparkDF.show(truncate=False)
```

![캡처6](https://user-images.githubusercontent.com/69948723/98310439-47236680-2010-11eb-85aa-a37ca6c06dc6.JPG)



### `Spark의 DataFrame 객체를 Pandas의 DataFrame 객체로 변환하기`

``` python
pandasDF = pysparkDF.toPandas()
print(type(pandasDF))
print(pandasDF)
```

![캡처7](https://user-images.githubusercontent.com/69948723/98310492-70dc8d80-2010-11eb-82ee-dd06a37e1cee.JPG)