## day3: Dataframe

### `1.iris 라는 데이터셋이 몇 개의 관측치를 가지고 있으며 어떠한 변수들을 가지고 있는지 확인하려 한다. 이 때 사용되는 R코드를 작성하시오. `

``` R
str(iris)
```



### `2.  c() 함수로 먼저 벡터를 생성한 다음 data.frame()사용해서 다음과 같이 구성되는 데이터 프레임 df3를 만들어 출력해 본다.(제품명이 팩터형이 되지 않게 한다.)`

>**제품명  가격   판매량**
>
>​       **사과   1800   24**
>
>​       **딸기   1500   38**
>
>​       **수박   3000   13**

``` R
제품명 <- c('사과', '딸기', '수박')
가격 <- c(1800, 1500, 3000)
판매량 <- c(24, 38, 13)
df3 <- data.frame(제품명, 가격, 판매량, stringsAsFactors = F)
```

### `3. 앞에서 만든 데이터 프레임을 이용해서 과일 가격 평균, 판매량 평균을 구하여 출력한다.`

``` R
sum(df3[, 2])/3; min(df3$가격)
sum(df3[, 3])/3; min(df3$판매량)
```



### `4. 다음 세 벡터를 이용하여 데이터프레임 df4를 생성하고 구조를 확인한다.`

>**name <- c(“Potter”, “Elsa”, “Gates”, “Wendy”, “Ben”)**
>
>**gender <- factor(c(“M”, “F”, “M”, “F”, “M”))**
>
>**math <- c(85, 76, 99, 88, 40)**

위에서 만든 데이터프레임에 대해 다음 작업을 수행하시오. 

>**(a) stat 변수를 추가하시오. stat <- c(76, 73, 95, 82, 35)**
>
>**(b) math 변수와 stat 변수의 합을 구하여 score 변수에 저장하시오.** 
>
>**(c) 논리 연산 인덱싱을 이용하여 score가 150 이상이면 A, 100 이상 150 미만이면 B, 70 이상 100 미만이면 C, 70 미만이면 D 등급을 부여하고 grade 변수에 저장하시오.** 

``` R
name <- c("Potter", "Elsa", "Gates", "Wendy", "Ben")
gender <- factor(c("M", "F", "M", "F", "M"))
math <- c(85, 76, 99, 88, 40)
df4 <- data.frame(name, gender, math);
df4
stat <- c(76, 73, 95, 82, 35)
# (a)
df4$stat <- stat
# (b)
df4$score <- df4$math + df4$stat
# (c)
df4$grade <-ifelse(df4$score >= 150,"A",
                  ifelse(df4$score >= 100,"B", 
                         ifelse(df4$score >= 70,"C","D")))
```



### `5.emp변수에 할당된 데이터프레임 객체의 구조를 점검한다. `

``` R
str(emp)
```



### `6. emp에서 3행, 4행, 5행만 출력한다.`

``` R
emp[c(3, 4, 5), ]
```



### `7. emp에서 4번열을 제외하고 출력하라.`

``` R
# 데이터프레임은 열 기준
emp[, -4]; emp[-4]
```



### `8. emp에서 ename 칼럼만 출력한다.`

``` R
emp["ename"]; emp$ename
```



### `9. emp에서 ename과 sal 칼럼만 출력한다.`

``` R
emp[, c("ename", "sal")]
subset(emp, sselect = c(ename, sal))
```



### `10. 업무가 SALESMAN인 사원의 이름, 월급, 직업을 출력하라.`

``` R
emp[emp$job == "SALESMAN", c("ename","sal", "job")]
```



### `11. 월급이 1000 이상이고 3000 이하인 사원들의 이름, 월급, 부서번호를 출력하라.`

``` R
emp[emp$sal>=1000 & emp$sal <=3000, c("ename","sal", "deptno")]
```



### `12. emp에서 직업이 ANALYST가 아닌 사원들의 이름, 직업, 월급을 출력하라.`

``` R
emp[!emp$job == "ANALYST", c("ename", "job", "sal")]
```



### `13. emp에서 직업이 SALESMAN 이거나 ANALYST인 사원들의 이름, 직업을 출력하라.`

``` R
emp[emp$job == "SALESMAN" | emp$job == "ANALYST", c("ename", "job")]
```



### `14. emp에서 커미션이 정해지지 않은 직원의 이름과 월급 정보를 출력하라.`

``` R
emp[is.na(emp$comm), c("ename", "sal")]
```



### `15. 월급이 적은 순으로 모든 직원 정보를 출력한다.`

``` R
emp[order(emp$sa, decreasing = F),]
```



### `16. emp의 행과 열의 개수를 점검한다.`

``` R
dim(emp)
```



###  `17. 월급이 많은 순서대로 모든 직원 정보를 출력하라.`

``` R
emp[order(emp$sa, decreasing = T),]
```

