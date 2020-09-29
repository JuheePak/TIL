## day 18: dplyr package

### MariaDB 에서 emp 테이블의 내용을 읽어서 emp 변수를 생성한다.

### `1. comm 컬럼값이 0 보다 적으면 NA 값으로 변경한다.`

``` R
library(rJava)
library(RJDBC)
library(DBI)
library(dplyr)

drv <- JDBC(driverClass = 'org.mariadb.jdbc.Driver', 'mariadb-java-client-2.6.2.jar')
conn <- dbConnect(drv, 'jdbc:mariadb://127.0.0.1:3306/work', 'scott', 'tiger')
emp <- dbReadTable(conn, 'emp')

# 커미션 음수인 사람 na처리
emp %>% mutate(comm = ifelse(comm < 0, NA, comm)) -> emp
# king의 mgr 음수 na 처리
emp %>% mutate(mgr = ifelse(mgr < 0, NA, mgr)) -> emp
```



### `2. 업무가 MANAGER 인 직원들의 정보를 출력한다. `

``` R
emp %>% filter(job == 'MANAGER')
```



### `3. emp 에서 사번, 이름, 월급을 출력한다.`

``` R
emp %>% select(empno, ename, sal)
```



### `4. emp 에서 사번만 빼고 출력한다.`

``` R
emp %>% select(-empno)
```



### `5. emp 에서 ename 과 sal컬럼만 출력한다.`

``` R
emp %>% select(ename, sal)
```



### `6. 업무별 직원수를 출력한다.`

``` R
emp %>% count(job)  
```



### `7. 월급이 1000 이상이고 3000이하인 사원들의 이름, 월급, 부서번호를 출력한다.`

``` R
emp %>% filter(sal >= 1000 & sal <= 3000) %>% select(ename, sal, empno)
```



### `8. emp 에서 업무이 ANALYST 가 아닌 사원들의 이름, 직업, 월급을 출력한다.`

``` R
emp %>% filter(job != 'ANALYST') %>% select(ename, job, empno)
```



### `9. emp 에서 업무가 SALESMAN 이거나 ANALYST 인 사원들의 이름, 직업을 출력한다.`

``` R
emp %>% filter(job == 'ANALYST' | job == 'SALESMAN') %>% select(ename, job)
```



### `10. 부서별 직원들 월급의 합을 출력한다.`

``` R
emp %>% group_by(deptno) %>% summarise(sal = sum(sal)) 
```



### `11. 월급이 적은 순으로 모든 직원 정보를 출력한다.`

``` R
emp %>% arrange(sal)
```



### `12. 월급이 제일 많은 직원의 정보를 출력한다.`

``` R
emp %>% arrange(desc(sal)) %>% head(1)
```



### `13. 직원들의 월급을 보관하고 있는 컬럼의 컬럼명을 sal에서 salary 로 변경하고 커미션 정보 저장한 컬럼의 컬럼명를 comm 에서 commrate 로 변경한 후 empnew 라는 새로운 데이터셋을 생성한다.`

``` R
empnew <- emp %>% rename("salary"="sal") %>% rename("commrate" = "comm")
empnew
```



### `14.가장 많은 인원이 일하고 있는 부서 번호를 출력한다. `

``` R
emp %>% count(deptno) %>%
  arrange(desc(n)) %>% head(1) %>% select(deptno)
```



### `15. 각 직원들 이름의 문자 길이를 저장하는 enamelength 라는 컬럼을 추가한 다음에 이름 길이가 짧은 순으로 직원의 이름을 출력한다.`

``` R
emp %>% mutate(enamelength = nchar(ename)) %>%
  arrange(enamelength) %>% select(ename)
```



### `16. 커미션이 정해진 직원들의 명수를 출력한다.`

``` R
emp %>%
  mutate(who_has_comm = ifelse (!is.na(comm), "커미션 정해진 사람", "커미션 정해지지 않은 사람")) %>%
  count(who_has_comm) %>%
  filter(who_has_comm == '커미션 정해진 사람')

#or
emp %>% filter(!is.na(comm)) %>% count
```

