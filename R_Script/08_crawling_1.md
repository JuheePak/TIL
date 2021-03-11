## day 8: 정적크롤링

### `1. 다음영화 사이트에 올려진 (http://movie.daum.net/) 댓글에 대하여 **고객 평점과 리뷰글**을 1페이지(10개)만 스크래핑하여 데이터프레임 형식으로 만들어 "daummovie1.csv" 로 저장한다.`

> https://movie.daum.net/moviedb/grade?movieId=131576

### `R 코드는 movie1.R 로 생성하여 csv 파일과 함께 제출하라.`

``` R
library(rvest)

text<-NULL; point<-NULL; review<-NULL
url<- "https://movie.daum.net/moviedb/grade?movieId=131576"
text <- read_html(url,  encoding="UTF-8")
text

#평점
nodes <- html_nodes(text, ".emph_grade")
# nodes <- html_nodes(text, "div.ranking_grade > em")
point <- html_text(nodes)
point

#리뷰
nodes <- html_nodes(text, " .desc_review")
nodes <- html_text(nodes, trim=TRUE)
nodes
review <- nodes[nchar(nodes) > 0]
review <- gsub("[\r]"," ", review) # \r 제거
review

page <- data.frame(point, review)
View(page)
write.csv(page, "daummovie1.csv")
```

### `2. 이번에는 평점과 리뷰글을 5페이지까지 크롤링하고 평점과 댓글을 스크래핑하여 데이터프레임으로 만들어 "daummovie2.csv" 로 저장한다.`

``` R
library(rvest)

site <- "https://movie.daum.net/moviedb/grade?movieId=131576&type=netizen&page="
text <- NULL; point <- NULL; review <- NULL; movie.review <-NULL; temp <- NULL
for(i in 1:5) {
  url <- paste(site, i, sep="")
  text <- read_html(url,  encoding="UTF-8")
  nodes <- html_nodes(text, ".emph_grade")
  point <- html_text(nodes)
  
  temp <- html_nodes(text, ".desc_review")
  review <- html_text(temp, trim=TRUE)
  review <- gsub("[\r]"," ", review) # \r 제거
  review
  
  if(length(review) == 10) {
    page <- data.frame(point, review)
    movie.review <- rbind(movie.review, page) # 공백도 그냥 집어넣음
  }
}

write.csv(movie.review, "daummovie2.csv")
```



### `3. 이번에는 평점과 리뷰글을 모든 페이지 크롤링하고 평점과 댓글을 스크래핑하여 데이터프레임으로 만들어 "daummovie3.csv" 로 저장한다.`

``` R
library(rvest)

site <- "https://movie.daum.net/moviedb/grade?movieId=131576&type=netizen&page="
text <- NULL; point <- NULL; review <- NULL; movie.review <-NULL; temp <- NULL

# 마지막으로 크롤링 할 페이지 수 구하기
cnt_site <- "https://movie.daum.net/moviedb/grade?movieId=131576&type=netizen&page=1"
cnt_nodes <- read_html(url,  encoding="UTF-8")
cnt_nodes <- html_nodes(cnt_nodes, ".txt_menu") # 어느 페이지든 나와있는 총 평점수(리뷰값과 다르게 평점은 필수값이다.)
cnt <- html_text(cnt_nodes)
cnt <- gsub('[(,)]',"",cnt) # 필요없는 문자열제거

cnt <- as.numeric(cnt) / 10 #한 페이지 최대 리뷰글(코멘트 여부 상관X)수는 10개.
page_cnt <- ceiling(cnt); page_cnt # 반올림함. (최대 리뷰수 10개를 넘지 않는다고 해도 크롤링 해야한다.)


for(i in 1:page_cnt) {
  url <- paste(site, i, sep="")
  text <- read_html(url,  encoding="UTF-8")
  nodes <- html_nodes(text, ".emph_grade")
  point <- html_text(nodes)
  
  temp <- html_nodes(text, ".desc_review")
  review <- html_text(temp, trim=TRUE)
  review <- gsub("[\r]"," ", review) # \r 제거
  review
  
  if(length(review) == 10) {
    page <- data.frame(point, review)
    movie.review <- rbind(movie.review, page) # 공백도 그냥 집어넣음
  }
}

View(movie.review)
write.csv(movie.review, "daummovie3.csv")
```

