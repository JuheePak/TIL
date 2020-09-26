## day 15:  data processing

### `1. 1부터 26사이의 값들 중에서 10개를 추출하여 v라는 변수에 저장한다. 추출된 숫자에 해당하는 알파벳 대문자를 원소값으로 구성된 벡터를 생성하는 코드를 작성하시오. 단, 숫자 벡터를 알파벳 대문자로 구성된 벡터를 리턴하는 기능을 반드시 sapply() 함수로 해결해야 한다.`

``` R
v <- sample(1:26, 10); v
#v1 <- rawToChar(as.raw(v[1]+64)); v1


myf <- function(x){
    for (i in 1:length(x)){
      return(rawToChar(as.raw(x[i]+64)))
      #return(LETTERS[x])
  }
}

sapply(v, myf)
```



### `2. 제시된 memo.txt 파일을 행 단위로 읽어서 벡터를 리턴한다. 벡터를 구성하고 있는 각 원소들의 내용을 확인한 후에 아래에 제시된 결과로 변경되도록 문자 또는 문자열 변경을 시도한다. (gsub() 사용) 원소마다 변경해야 하는 룰이 다르므로 원소마다 처리한다. 처리된 결과를 memo_new.txt 파일에 저장한다. (write() 함수 사용)

> **당신의 믿음은 곧 당신의 생각이 되고, 당신의 생각은 곧 당신이 내뱉는 말이 되고, 당신이 내뱉는 말은 곧 당신의 행동이 되고, 당신의 행동은 곧 당신의 습관이 되고, 당신의 습관은 곧 당신의 가치관이 되고, 당신의 가치관은 곧 당신의 운명이 된다.**
>
> **중요한 일을 절대 E메일로 보내지 마라!**
>
> **가장 훌륭한 일은 모험과 도전정신으로 이루어진다.**
>
> **남들이 나와 같지 않다는 점을 인정하라.**
>
> **매일 아침 삶의 목표를 생각하며 일어나라.**
>
> **위대한일을하는유일한방법은바로당신이하는일을사랑하는것입니다.**
>
> **you 타협(정착)하지 마세요. 왜냐하면, 당신의 마음이 하는 모든 것이 그렇듯이, 그 일을 찾게 되면 당신은 마음으로 알게 될 겁니다. ok?**

``` R
memo <- readLines('data/memo.txt', encoding = 'UTF-8'); memo

memo1 <- gsub("[$&!#@%]", "", memo[1]); memo1

memo2 <- gsub("e", "E", memo[2]); memo2

memo3 <- gsub("[[:digit:]]", "", memo[3]); memo3
# gsub("[0-9]", "", memo[3])
# gsub("[44567891234", "", memo[3])
# gsub("\\d", "", memo[3])

memo4 <- gsub("[[:lower:][:upper:]]", "", memo[4]); memo4

memo5 <- gsub("[0-9]", "", memo[5]); memo5
memo5 <- gsub("[<>!]", "", memo5); memo5

memo6 <- gsub("[[:blank:]]", "", memo[6]); memo6

memo7 <- gsub("YOU", "you", memo[7]); memo7
memo7 <- gsub("OK", "ok", memo7); memo7
#OR
memo7 <- gsub("O", "o", memo[7]); memo7
memo7 <- gsub("Y", "y", memo7); memo7
memo7 <- gsub("U", "u", memo7); memo7
memo7 <- gsub("K", "k", memo7); memo7
#OR
memo7 <- gsub("Y.+U", "you", memo[7]); memo7
memo7 <- gsub("OK", "ok", memo7); memo7

mymemo <- c(memo1, memo2, memo3, memo4, memo5, memo6, memo7)
mymemo


write(mymemo, "memo_new.txt")
```

