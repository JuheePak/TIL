## day 21: Text mining

### `1. 이전에 yes24 사이트에서 크롤링 한 책 명견만리의 리뷰를 저장한 "yes24.txt" 파일의 내용을 읽고 명사만 뽑아내 많이 등장한 단어 순으로 다음과 같이 워드클라우딩 하는 R 코드를 작성하여 wc.R로, 그 결과는 wc.html로 저장하라.`

```R
result<-wordcloud2(……………………………………)
library("htmlwidgets") # 없으면 설치
saveWidget(result,"wc.html",title="WORDCLOUD 실습", selfcontained = F)


#-----------위에 설치하고 진행-------------------

library(KoNLP)
library(htmlwidgets)
library(wordcloud)
library(wordcloud2)

word_data <- readLines("yes24.txt")
word_data2 <- extractNoun(word_data)
undata <- unlist(word_data2)
word_table <- table(undata)
word_table

undata2 <- Filter(function(x) {nchar(x) >= 2}, undata)
word_table2 <- table(undata2)

final <- sort(word_table2, decreasing = T)
head(final, 10)

#figPath = system.file("book.png", package = "wordcloud2")
#result <- wordcloud2(final, figPath = figPath, size = 1.5, fontFamily = "휴먼옛체")

result <- wordcloud2(final, fontFamily = "휴먼옛체")
saveWidget(result, "wc.html", title="WORDCLOUD 실습", selfcontained = F)
```

