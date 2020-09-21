## day 10: 정적크롤링

### `1. https://comic.naver.com/genre/bestChallenge.nhn 사이트의 콘텐츠 내용을 추출하고 comicName,  comicSummary, comicGrade 열명으로 DataFrame을 생성하여 navercomic.csv로 저장하고 소스는 navercomic.R로 저장한다. 모든 페이지를 크롤링하고 스크래핑한다.`

> comicName: 웹툰 이름
>
> comicSummary: 요약정보
>
> comicGrade: 평점

``` R
library(rvest)

site <- "https://comic.naver.com/genre/bestChallenge.nhn?&page="
comicName<-NULL; comicSummary<-NULL; comicGrade<-NULL; navercomic <- NULL;

pageNum <- 1 
# 0이 아닌 1로 시작하는 이유는 cnt는 페이지 하단의 이전, 다음 버튼 총 2개가 아니면 break 걸리는데
# 첫번째 페이지는 '이전' 버튼이 없고 마지막 페이지는 '다음' 버튼이 없음.
# 마지막 페이지인 124를 넘어가도 페이지는 그대로 유지되어, 페이지 수가 124가 넘어가면 사라지는 것을 찾음 -> '다음'버튼

cnt <- 24 # 첫번째 페이지에 있는 웹툰 작가 수
while (TRUE){
  pageNum <- pageNum + 1
  url <- paste(site, pageNum, sep="")
  text <- read_html(url, encoding="UTF-8")
  nodes <- html_nodes(text, ".user")
  user <- html_text(nodes, trim = TRUE)
  
  nodes <- html_nodes(text, ".cnt_page") # 다음 버튼, 맨 마지막 페이지 제외 항상 있음
  next_button <- html_text(nodes, trim = TRUE)
  
  if (length(next_button) != 2){ # 이전, 다음 버튼 두개 다 없으면(마지막 페이지)
    cnt <- cnt + 18 # 마지막 페이지에 있는 웹툰 작가 수
    break
  } else {
    cnt <- cnt + as.numeric(length(user))
  }
}
print(cnt) #2970 개의 웹툰작품
cnt <- as.numeric(cnt) / 24 # 123.75
page_cnt <- ceiling(cnt); page_cnt #올림

for(i in 1:page_cnt) {
  url <- paste(site, i, sep="")
  text <- read_html(url,  encoding="UTF-8")
  
  # 타이틀
  nodes <- html_nodes(text, "tr > td > div.challengeInfo > h6 > a")
  comicName <- html_text(nodes, trim=TRUE); comicName
  
  # 평점
  nodes <- html_nodes(text, "div.rating_type > strong"); nodes
  comicGrade <- html_text(nodes); comicGrade
  
  # 요약 정보
  nodes <- html_nodes(text, "div.summary"); nodes
  comicSummary <- html_text(nodes); comicSummary
  
  if(length(comicName) != 0) {
    page <- data.frame(comicName, comicGrade, comicSummary)
    navercomic <- rbind(navercomic, page)
  }
}

View(navercomic)
write.csv(navercomic, "navercomic.csv")
```











