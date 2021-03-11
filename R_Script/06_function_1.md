## day 6: function

### `1.다음 사양의 함수 exam1( )을 생성한다.`

> **매개변수 : 없음**
>
> **리턴 값 : 1개**
>
> **기능 : “Aa” “Bb” ~ “Zz” 등으로 구성된 벡터를 리턴한다.**
>
> **결과 출력은 함수를 호출한 다음 리턴값을 받아서 호출한 쪽에서 한다.**

``` R
exam1 <- function() {
  a <- paste(LETTERS,letters,sep="")
  return (a)
}
print(exam1())
```



### `2. 다음 사양의 함수 exam2( )을 생성한다.`

> **매개변수 : 1 개**
>
> **리턴 값 : 1개**
>
> **기능 : 아규먼트로 숫자 한 개를 받는다.** 
>
> **1 부터 이 숫자 값까지의 합을 구해서 리턴한다.**
>
> **결과 출력은 함수를 호출한 다음 리턴값을 받아서 호출한 쪽에서 한다.**

``` R
exam2 <- function(x) {
  sum <- 0;
  for(item in x) {
    sum <- sum(seq(1, item, 1))
}
  return(sum)
}
print(exam2(1))

#or

exam2 <- function(num) {
  sum <- 0
  for(i in 1:num){
    sum <- sum+i
  }
  return(sum)
}
```



### `3. 다음 사양의 함수 exam3( )을 생성한다.`

> **매개변수 : 2 개**
> **리턴 값 :  1개**
> **기능 : 전달받은 2개의 데이터 중에서 큰 값에서 작은 값의 차를 리턴하고 두 값이 동일하면 0 을 리턴한다.**
> 예를 들어,
> **10, 20 이 전달되면 ---> 10 리턴**
> **20, 5 가 전달되면 ---> 15 리턴**
> **5, 30 이 전달되면 ---> 25 리턴**
> **6, 3 이 전달되면  ---> 3 리턴**
>
> 결과 출력은 함수를 호출한 다음 리턴값을 받아서 호출한 쪽에서 한다.

``` R
exam3 <- function(p1, p2) {
  if (p1 > p2){
    return (p1-p2)
  } else if (p1 < p2){
    return (p2-p1)
  } else if (p1 == p2) {
    return (0)
  }
}
print(exam3(p1=2, p2=10))
```



### `4. 다음 사양의 함수 exam4( )를 생성한다.`

> **매개변수 : 3 개**
>
> **리턴 값 : 1개**
>
> **기능 : 아규먼트를 숫자 연산자 숫자 순으로 전달받는다. (연산자는 +, -, *, %/%, %% 를 받는 것으로 정한다.) 전달된 두 개의 숫자에 대하여 연산을 처리하고 그 결과를 리턴한다.**
>
> 단, 다른 연산자가 전달되면 "규격의 연산자만 전달하세요"를 리턴한다.
>
> %/% 와 %% 가 전달된 경우에 한해서 첫 번째 숫자가 0이면 "오류1" 이라고 리턴한다.
>
> %/% 와 %% 가 전달된 경우에 한해서 두 번째 숫자가 0이면 "오류2" 라고 리턴한다.
>
> 함수를 호출하여 리턴된 결과를 출력하는 것은 호출한 쪽에서 한다.

 

``` R
exam4 <- function (a, mycal, c) {
  if (mycal == '+'){
    return (a + c)
  } else if (mycal == '*'){
    return (a * c)
  } else if (mycal == '-'){
    return (a - c)
  } else if (mycal == '%/%'){
    if (a != 0)
      return (a %/% c)
    else 
      return ("오류1")
  } else if (mycal == '%%') {
    if (c != 0)
      return (a %% c)
    else
      return ("오류2")
  } else {
    return ("규격의 연산자만 전달하세요.")
  }
}

print(exam4(a=4, mycal='%%', c=0))
```



### `5. 다음 사양의 함수 exam5( )을 생성한다.`

> 매개변수: 2 개(한 개는 필수, 또 다른 한 개는 선택(기본값 설정)
>
> 리턴 값: 없음 (NULL 리턴) 
>
> 기능: 첫 번째 아규먼트는 숫자를 두번째 아규먼트는 문자를 입력받아서 숫자의 개수만큼 문자를 출력하는 기능을 처리한다.(행바꿈X) 문자가 전달되지 않으면 기본값은 "**#**" 로 처리한다. 숫자로 음의 값이 전달되면 아무것도 출력하지 않는다.

``` R
exam5 <- function (..., n='#') {
  data <- list(...)
  for (i in data) {
    if (is.numeric(i)){
      if (i > 0)
        cat(rep(n, times=length(i)), sep='')
      else
        return ()
    } else {
      n <- i
      cat(rep(n, times=length(i)), sep='')
    }
  }
}
exam5(6, 7, 8, n='^')

# or
exam5 <- function(p1, p2='#'){
  if (p1>0) {
    for (num in 1:p1){
      cat(p2)
    }
    cat('\n')
  }
}
exam5(5, '$')
```



### `6. 다음 사양의 함수 exam6( )를 생성한다.`

> 매개변수: 1 개
>
> 리턴 값: 없음(NULL 리턴)
>
> 기능: 아규먼트로 전달되는 벡터에는 학생들의 점수(0~100)가 들어 있다. 점수에 따라서 결과를 출력한다.
>
> ​      **85~100 "상"**
>
> ​      **70~84 "중"**
>
> ​      **~69  "하"**
>
> 출력형식 : **"xx 점은 x등급입니다."** 
>
> NA 값이 존재하는 경우엔 **"NA 는 처리불가"** 를 출력한다.
>
> 모든 출력은 print() 함수를 사용한다.

**exam6(c(80, 50, 70, 66, NA, 35))**

``` R
exam6 <- function (...) {
  data <- c(...)
  for (i in data) {
    if (!is.na(i)) {
      if (85 <= i &  i<=100)
        print(paste(i, "점은 상등급입니다."))
      else if (i >= 70)
        print(paste(i, "점은 중등급입니다."))
      else if (i <= 69)
        print(paste(i, "점은 하등급입니다."))
    } else  {
        print("NA는 처리불가")
    }
  }
}

exam6(c(80, 50, 70, 66, NA, 35))

# or

exam6 <- function (...) {
  data <- c(...)
  for (score in data){
    if(is.na(score)) print("NA는 처리불가")
    else{
      if(score>=85) grade <- "상"
      else if(score >=70) grade <-'중'
      else grade <- '하'
      print(paste(score,'점은',grade,'등급입니다.',sep=''))
    }
  }
}

exam6(80, 50, 70, 66, NA, 35)

```



 