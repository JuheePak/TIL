## day 16: data_processing

### `1. R언어로 내가 태어난 요일을 다음 형식으로 출력해보자.`

> XXX는 X요일에 태어났어요

``` R
name <- '주희'
bday <- as.POSIXlt("1993-06-15")
paste(name, "는 ", weekdays(bday),"에 태어났어요", sep='')
```



### `2. 내가 태어난지 며칠이 지났는지 다음 형식으로 출력해 보자.`

> 오늘은 XXXX년 XX월 XX일이고 내가 태어난지 XXXX일 째 되는 날이다.

``` R
tmp<-Sys.Date()
year<-format(tmp,'%Y')
month<-format(tmp,'%m')
day<-format(tmp,'%d')
weekday<-format(tmp,'%A')
mydays <- as.Date("2020/09/23") - as.Date("1993/06/15")

paste("오늘은 ",year,"년 ",month,"월 ",day,
      "일 이고 내가 태어난지 ", mydays, "일째되는 날이당", sep="")

```



### `3.현재시간을 기준으로 년월일시분 정보를 출력해 보자. `

> XXXX년 XX월 XX일 XX시 XX분 XX초

```` R
today <- Sys.time()
format(today, "%Y년 %m월 %d일 %H시 %M분 %S초")
````



### `4. 텍스트 '12/25/2020 23:59:59', '1/25/2021 23:59:59', '2/25/2021 23:59:59'를 데이터프레임의 datetime 변수에 저장한 후 이를 날짜 형식(POSIXlt 객체)으로 변환한다.`

```R
datetime <- c('12/25/2020 23:59:59', '1/25/2021 23:59:59', '2/25/2021 23:59:59')
myd1 <- strptime(as.Date(datetime[1], format='%m/%d/%Y'), "%Y-%m-%d")
myd2 <- strptime(as.Date(datetime[2], format='%m/%d/%Y'), "%Y-%m-%d")
myd3 <- strptime(as.Date(datetime[3], format='%m/%d/%Y'), "%Y-%m-%d")
str(myd1)
datetime <- c(myd1, myd2, myd3); datetime
```



### `5. 2020년 6월 1일부터 7일간의 월, 일, 요일을 seq() 함수를 이용하여 생성하고 다음과 같은 형식으로 출력한다. `

> "월-0601" "화-0602" "수-0603" "목-0604" "금-0605" "토-0606" "일-0607"

``` R
days <- seq(20200601, 20200607, 1)
md <- format((strptime(days, "%Y%m%d")), "%m%d")
weekday <-format((strptime(days, "%Y%m%d")),'%a')

for (i in 1:length(md)){
  cat('"', weekday[i],"-",md[i],'"', sep='')
}

#or

start <- as.Date("2020-06-01")
end <- as.Date("2020-06-07")
day <- seq(start, end, 1)
format(day, "%a-%m%d")

```



### `6. 'Happy', 'Birthday', 'to', You'로 구성된 텍스트 벡터 v1 생성한 후 벡터의 길이와 문자 개수의 합을 계산한다. `

``` R
v1 <- c('Happy', 'Birthday', 'to', 'You')
mysum <- length(v1) + sum(nchar(v1))
```



### `7.  6번 문제에서 생성한 텍스트 벡터 v1의 개별 원소들을 연결하여 다음과 같은 텍스트 벡터를 생성한다. 연결된 새로운 텍스트 벡터의 길이와 문자 개수의 합을 계산한다.`

> "Happy Birthday to You"

``` R
v2 <- paste('Happy', 'Birthday', 'to', 'You')
mysum2 <- length(v2) + sum(nchar(v2))
```



### `8. paste() 함수와 LETTERS 상수 벡터를 이용하여 다음과 같은 문자 벡터를 생성한다(첫 번째 벡터는 문자와 숫자 사이에 공백이 있으며, 두 번째 벡터는 문자와 숫자가 서로 붙어 있음).`

> "A 1" "B 2" "C 3" "D 4" "E 5" "F 6" "G 7" "H 8" "I 9" "J 10"
>
>  "A1" "B2" "C3" "D4" "E5" "F6" "G7" "H8" "I9" "J10"

``` R
paste(LETTERS[1:10], 1:10)
paste(LETTERS[1:10], 1:10, sep='')
#or
paste0(LETTERS[1:10], 1:10)
```



### `9. 텍스트 'Good Morning'을 분할하여 다음과 같은 리스트 형식으로 출력한다.`

> ​       [[1]]
>
> ​       [1] "Good"
>
> ​       [[2]]
>
> ​       [1] "Morning"

``` R
t1 <- substr("Good Morning", start=1, stop=4)
t2 <- substr("Good Morning", start=6, stop=12)
list(t1, t2)


#or
txt <- c("Good Morning")
txt2 <- unlist(strsplit(txt, split=' '))
strsplit(txt2, split=' ')
```



### `10. 다음 텍스트 벡터를 단어 단위로 분할한다. 단, 모든 쉼표(,)와 하이픈(-)을 제거한다.`

> c("Yesterday is history, tommrrow is a mystery, today is a gift!", 
>
> ​              "That's why we call it the present – from kung fu Panda")

``` R
myV <- c("Yesterday is history, tommrrow is a mystery, today is a gift!", 
  "That's why we call it the present - from kung fu Panda")

myV <- gsub("[,-]", "", myV)
myV <- gsub("\\s+", ' ', myV) #다중공백제거
myV <- gsub("\\s{2,}", ' ', myV) #다중공백제거
strsplit(x= myV, split= " ")

```



### `11. 다음 주민등록번호 세 개를 ssn 변수에 저장하고, 뒤 일곱 자리의 숫자를 '*******'으로 대체한다.`

> "941215-1234567" "850605-2345678" "760830-1357913"

``` R
ssn <- c("941215-1234567", "850605-2345678", "760830-1357913")
ssn1 <- gsub("-[0-9][0-9][0-9][0-9][0-9][0-9][0-9]", "-*******", ssn[1]); ssn1
ssn2 <- gsub("-[0-9][0-9][0-9][0-9][0-9][0-9][0-9]", "-*******", ssn[2]); ssn2
ssn3 <- gsub("-[0-9][0-9][0-9][0-9][0-9][0-9][0-9]", "-*******", ssn[3]); ssn3

#OR

ssn <- c("941215-1234567", "850605-2345678", "760830-1357913")
substr(ssn, nchar(ssn)-6, nchar(ssn)) <-"*******"
print(ssn)

```



### `12. 다음 문자열을 s1 변수에 저장한 다음 요구 사항대로 처리한다.`

> "@^^@Have a nice day!! 좋은 하루!! 오늘도 100점 하루...."

### `(1) 한글만 삭제하여 r1 에 저장 한다. `

### `(2) 특수문자들을 삭제하여 r2 에 저장 한다.`

### `(3) 한글과 특수문자들을 삭제하여 r3 에 저장 한다.`

### `(4) 100을 '백'으로 변환하여 r4에 저장 한다.`

``` R

s1 <- c("@^^@Have a nice day!! 좋은 하루!! 오늘도 100점 하루....")

#(1)
r1 <- gsub("[가-힣]", "", s1); r1

#(2)
r2 <- gsub("[[:punct:]]", "", s1); r2

#(3)
r3 <- gsub("[가-힣@^!.]", "", s1); r3

#(4)
r4 <- gsub("100", "백", s1); r4
```

