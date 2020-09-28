## day 17: chart

### `1.  제품당 클릭 갯수에 대한 데이터를 가지고 다음 조건으로 그래프를 그린다.  옆의 그림처럼 세로 바 그래프를 칼라는 terrain.colors 칼라로 설정한다.`

> 그래프 메인 제목:  "세로바 그래프 실습"
>
> clicklog1.png 에 저장한다.

![image-20200928134208782](C:\Users\juhee\TIL\R Script\image-20200928134208782.png)

``` R
barplot(table(productdf$pid), main="세로바 그래프 실습", 
        xlab="상품ID", ylab="클릭수", col=terrain.colors(10))

dev.copy(png, "clicklog1.png")
dev.off()
```



### `2.데이터는 MariaDB에 저장된 productlog 라는 테이블의 데이터를 모두 읽어와서 다음과 같이 상품이 클릭된 시간 정보를 가지고   파이그래프를 그리며 칼라는 자율이다.  `

> 그래프 메인 제목 : "파이그래프 실습"
>
> 그래프는 clicklog2.png 에 저장한다.

![image-20200928134321917](C:\Users\juhee\TIL\R Script\image-20200928134321917.png)

``` R
ctime <- productdf$clicktime
productdf$c <- as.numeric(substr(ctime, 9, 10))
productdf
cc <- c(0~1, 1~2, 2~3, 3~4, 4~5, 5~6, 8~9, 9~10, 10~11, 11~12, 12~13, 13~14, 14~15, 15~16, 16~17, 17~18, 18~19)
pie(table(productdf$c), main="파이그래프 실습", labels=cc,
    clockwise=F, col=rainbow(10), radius=1.1)

dev.copy(png, "clicklog2.png")
dev.off()
```



### `3.수업시간에 다뤘던 성적데이터를 가지고 다음과 같은 그래프를 R로 구현해 본다. 그래프는 clicklog3.png 에 저장한다.`

![image-20200928134420367](C:\Users\juhee\TIL\R Script\image-20200928134420367.png)



``` R
(성적 <- read.table("data/성적.txt", header=TRUE))
성적2 <- 성적[,3:5]
boxplot(성적2, axes=F, col=topo.colors(3))
axis(1, at=1:3, lab=names(성적2))
axis(2, at=seq(2, 10, 2))
title("과목별 성적 분포", cex.main=2, col.main="orange")
box()

dev.copy(png, "clicklog3.png")
dev.off()
```

