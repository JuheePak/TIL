## day 5: 제어문

### `1. grade 라는 변수에 1부터 6사이의 난수를 추출하여 저장한다. `

>  grade 의 값이 1 또는 2 또는 3이면 다음 결과를 출력한다.
>
>   **"x 학년은 저학년입니다."**
>
>   grade 의 값이 4 또는 5 또는 6이면 다음 결과를 출력한다.
>
>   **"x 학년은 고학년입니다."**

``` R
grade <- sample(1:6, 1)
if(grade<=3){
  cat(grade,"학년은 저학년입니다.","\n")
}else{
  cat(grade,"학년은 고학년입니다.","\n")
}
```



### `2. choice 라는 변수에 1부터 5사이의 난수를 추출하여 저장한다. `

> 추출된 값이 1이면 300 과 50 의 덧셈 연산을 처리한다.
>
> 추출된 값이 2이면 300 과 50 의 뺄셈 연산을 처리한다.
>
> 추출된 값이 3이면 300 과 50 의 곱셈 연산을 처리한다.
>
> 추출된 값이 4이면 300 과 50 의 나눗셈 연산을 처리한다.
>
> 추출된 값이 5이면 300 과 50 의 나머지 연산을 처리한다.
>
> 출력 형식(단, 출력문장은 한 번만 구현한다.)
>
> **결과값 : XX**

``` R
choice <- sample(1:5,1)
x1 <- 300
y1 <- 50
myresult <- 0
if (choice == 1){
  myresult <- x1+y1
}else if (choice == 2){
  myresult <- x1-y1
}else if (choice == 3){
  myresult <- x1*y1
}else if (choice == 4){
  myresult <- x1/y1
}else if (choice == 5){
  myresult <- x1%%y1
}
cat('결과값:',myresult)

# or

result <- switch(EXPR=as.character(choice),
                 300+50, 300-50, 300*50, 300/50, 300%%50)
cat('결과값: ', result, sep='')

```

### `3.count 라는 변수에 3부터 10사이의 난수를 추출하여 저장한다. `

> **1부터 3사이의 난수를 추출한다.(deco)**
>
> **deco가 1이면 "*"을 count 값만큼 출력한다.**
>
> **deco가 2이면 "$"을 count 값만큼 출력한다.**
>
> **deco가 3이면 "#"을 count 값만큼 출력한다.**

``` R
count <- sample(3:10, 1)
deco <- sample(1:3, 1)

if (deco == 1) {
  cat(rep('*',times=count), sep='')
}else if (deco == 2){
  cat(rep('$',times=count), sep='')
}else if (deco == 3){
  cat(rep('#',times=count), sep='')
}
```



### `4. switch() 함수로 문제를 해결한다.`

> **score 라는 변수에 0~100 사이의 난수를 저장한다.**
>
> **score 의 값이 90~100 이면 level 변수에 “A 등급”을 저장한다.**
>
> **score 의 값이 80~89 이면 level 변수에 “B 등급”을 저장한다.**
>
> **score 의 값이 70~79 이면 level 변수에 “C 등급”을 저장한다.**
>
> **score 의 값이 60~69 이면 level 변수에 “D 등급”을 저장한다.**
>
> **score 의 값이 59 이하면 level 변수에 “F 등급”을 저장한다.**
>
> 결과를 다음 형식으로 출력한다.
>
> **“xx 점은 x 등급입니다.”**

``` R
score <- sample(0:100, 1)
temp <- score %/% 10 #몫을 구하는 연산자
temp <- as.character(temp) 
  cat(score,"점은", switch(EXPR = temp, 
                         "10"=, "9"="A" ,"8"="B","7"="C","6"="D","F"),"등급 입니다.","\n")

```



### `5.다음과 같이 영문자 대문자와 소문자로 구성되는 원소들을 갖는 벡터 alpha 를 생성하여 벡터의 내용을 화면에 출력한다.`

> **“Aa” “Bb” …………………….. “Zz”**

``` R
alpha <- paste(LETTERS,letters,sep="")
alpha

# or
for (i in 1:length(letters)){
   print(paste(LETTERS[i],letters[i], sep=''))
}

# or
alpha <- vertor()
for (num in 1:26){
  alpha[num] <- paste(LETTERS[num], letters[num], sep='')
}
alpha

```

