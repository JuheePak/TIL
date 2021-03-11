## day 14: MariaDB

### `1. R이 내장하고 있는 iris 데이터셋의 구조와 상위 데이터 6개를 확인한다.`

```R
#라이브러리 불러오기
library("rJava")
library("RJDBC")
library("DBI")

#MariaDB 연결
drv <- JDBC(driverClass = 'org.mariadb.jdbc.Driver', 'mariadb-java-client-2.6.2.jar')
#JDBC url
conn <- dbConnect(drv, 'jdbc:mariadb://127.0.0.1:3306/work', 'scott', 'tiger')
#getwd()

head(iris, 6)
str(iris)

```



###  `2. (2) iris 데이터셋의 변수명을 다음과 같이 변경한다. `

### `변수명 : slength, swidth, plength, pwidth, species`

```R
names(iris) <- c("slength", "swidth", "plength", "pwidth", "species")
head(iris)
```



### `3. 변수명을 변경한 iris 를 MariaDB 서버에 iris 라는 테이블 명으로 저장한다.`

```R
#dbRemoveTable(conn,"iris")
dbWriteTable(conn, 'iris', iris[1:150, ])
```



### `4. iris 테이블의 모든 데이터를 읽어서 iris_all 에 저장한다.`

```R
query <- "select * from iris"
iris_all <- dbGetQuery(conn, query)
iris_all
```

### `5. iris 테이블에서 species 가 ‘setosa’ 인 데이터들만 추출하여 iris_setosa 에 저장한다.`

```R
query <- "select * from iris where species = 'setosa'"
iris_setosa <- dbGetQuery(conn, query)
iris_setosa
```

### `6. iris 테이블에서 species 가 ‘virginica’ 인 데이터들만 추출하여 iris_versicolor 에 저장한다. `

```R
query <- "select * from iris where species = 'versicolor'"
iris_versicolor <- dbGetQuery(conn, query)
iris_versicolor
```



### `7. iris 테이블에서 species 가 ‘virginica’ 인 데이터들만 추출하여 iris_virginica 에 저장한다.`

```R
query <- "select * from iris where species = 'virginica'"
iris_virginica <- dbGetQuery(conn, query)
iris_virginica
```



### `8. "data/product_click.log" 데이터 파일을 읽어서 productdf 라는 데이터 프레임을 생성한다.`

``` R
productdf <- read.table("data/product_click.log")
dbWriteTable(conn, 'productdf', productdf)
```



### `9. productdf 데이터셋의 변수명을 다음과 같이 변경한다. 변수명 : clicktime, pid`

```R
head(productdf)
str(productdf) #746
names(productdf) <- c("clicktime", "pid")
```



### `10. (10) 변수명을 변경한 productdb 를 MariaDB 서버에 productlog 라는 테이블 명으로 저장한다.`

``` R
dbWriteTable(conn, 'productlog', productdf)
```



### `11. 상품 id  가 ‘p003’ 인 데이터들만 추출하여 p003 이라는 변수에 저장한다.`

```R
query <- "select * from productlog where pid = 'p003'"
p003 <- dbGetQuery(conn, query)
p003
```



### `12. "data/emp.csv" 데이터 파일을 읽어서 emp 라는 데이터 프레임을 생성한다.`

### `13. emp 를 MariaDB 서버에 emp 라는 테이블 명으로 저장한다.`

``` R
#(12) #(13)
emp <- read.csv("data/emp.csv")
dbWriteTable(conn, 'emp', emp)

head(emp)
str(emp)
```



### `14.emp 테이블에서 월급이 높은 순으로 데이터를 읽어와서 result1 에 저장한다. `

``` R
query <- "select * from emp order by sal desc"
result1 <- dbGetQuery(conn, query)
result1
```



### `15. emp 테이블에서 입사한지 오래된 순으로 데이터를 읽어와서 result2 에 저장한다.`

``` R
query <- "select * from emp order by hiredate"
result2 <- dbGetQuery(conn, query)
result2
```



### `16. emp 테이블에서 월급이 2000 이상인 데이터를 읽어와서 result3 에 저장한다.`

``` R
query <- "select * from emp where sal >= 2000"
result3 <- dbGetQuery(conn, query)
result3
```



### `17. emp 테이블에서 월급이 2000 이상이고 3000 미만인 데이터를 읽어와서 result4 에 저장한다. `

``` R
query <- "select * from emp where 2000 <= sal && sal < 3000"
result4 <- dbGetQuery(conn, query)
result4
```

