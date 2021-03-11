## day 9: 정적크롤링

### `1. 다음에 제시된 웹 페이지는 다음뉴스의 랭킹페이지이다. (http://media.daum.net/ranking/popular/)이 페이지에서 각 뉴스의 제목과 이 뉴스를 올린 신문사명칭을 스크래핑(50개)하여 newstitle, newspapername 형식의 데이터프레임을 만들어 CSV 파일로 저장하라.`



``` R
library(rvest)

site <- "https://news.daum.net/ranking/popular/"
text <- NULL; newspapername <- NULL; newstitle <- NULL
text <- read_html(site,  encoding="UTF-8")
text

nodes <- html_nodes(text, "ul.list_news2 > li > div.cont_thumb > strong.tit_thumb > a.link_txt")
newstitle <- html_text(nodes)
newstitle


nodes <- html_nodes(text, ".tit_thumb > span")
nodes
newspapername <- html_text(nodes)
newspapername

page <- data.frame(newspapername, newstitle)
View(page)
write.csv(page, "daumnews.csv")
```



