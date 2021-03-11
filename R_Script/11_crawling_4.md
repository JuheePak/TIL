## day 11: 동적크롤링

### `1. 네이버의 블로그에서 “맛집” 이라는 단어가 들어간 글들을 검색하여 100개까지 추출한 다음 naverblog.txt 파일로 저장하시오. 단, XML 형식의 요청을 처리한다. `

``` R
library(httr)
library(rvest)
library(XML)
library(rtweet)
library(jsonlite)

rm(list=ls())
searchUrl<- "https://openapi.naver.com/v1/search/blog.xml"
Client_ID <- 
Client_Secret <- 
query <- URLencode(iconv("맛집","euc-kr","UTF-8"))
url <- paste0(searchUrl, "?query=", query, "&display=100")
doc <- GET(url, add_headers("Content_Type" = "application/xml",
                            "X-Naver-client-Id" = Client_ID, "X-naver-Client-Secret" = Client_Secret))

doc2 <- htmlParse(doc, encoding="UTF-8")
naverblog <- xpathSApply(doc2, "//item/description", xmlValue)
naverblog
naverblog <- gsub("</?b>", "", naverblog)  
naverblog <- gsub("&.+t;", "", naverblog)
naverblog

View(naverblog)
df<- data.frame(naverblog)
write.table(df, "naverblog.txt")
```



###  `2. 트위터에서 “코로나” 이라는 단어가 들어간 트윗 글들을 검색하여 100개까지 추출한 다음 twitter.txt 파일로 저장하시오. `

### `제거해야 하는 문자들과 데이터 값 : 특수문자, 영어, NA 값`

``` R
appname <- "covid19_twt"
api_key <- 
api_secret <- 
access_token <- 
access_token_secret <- 
twitter_token <- create_token(
  app = appname,
  consumer_key = api_key,
  consumer_secret = api_secret,
  access_token = access_token,
  access_secret = access_token_secret)

key <- "코로나"
key <- enc2utf8(key) #CP949 -> UTF-8 변경함수
result <- search_tweets(key, n=100, token = twitter_token)
str(result)
twitter <- gsub("[[:lower:][:upper:][:punct:][:cntrl:]]", "", result)
twitter <- twitter[!is.na(twitter)]
View(twitter)

df<- data.frame(twitter)
write.table(df, "twitter.txt")
```



### `3. 공공DB에서 360번 차량에 대하여 정보를 추출한 다음 노선ID, 노선길이, 기점, 종점, 배차간격을 다음 형식으로 저장하시오.`

> **[ 360번 버스정보 ]**
>
> **노선ID : xxx**
>
> **노선길이 : xxx**
>
> **기점 : xxx**
>
> **종점 : xxx**
>
> **배차간격 : xxx**
>
> **참고 : http://api.bus.go.kr/contents/sub02/getBusRouteList.html**

``` R
API_key  <- 
bus_No <- "360"
url <- paste("http://ws.bus.go.kr/api/rest/busRouteInfo/getBusRouteList?ServiceKey=", API_key, "&strSrch=", bus_No, sep="")
doc <- xmlParse(url, encoding="UTF-8")
top <- xmlRoot(doc) 
top
df <- xmlToDataFrame(getNodeSet(doc, "//itemList")) 
df 
str(df)
View(df) #100100057

bus360 <- df[1, ]
bus360 <- bus360[1, c("busRouteId","length", "stStationNm","edStationNm", "term")] 
names(bus360) <- c("노선ID", "노선길이", "기점", "종점", "배차간격")
View(bus360)
```

 

### `4. 네이버의 뉴스에서 “빅데이터” 라는 단어가 들어간 뉴스글들을 검색하여 100개까지 추출한 다음 뉴스 제목을 추출하여 navernews.txt 파일로 저장하시오. 단, JSON 형식의 요청을 처리한다. `

### `제거해야 하는 문자들 : <b>, </b>, &quot;, &gt;`

``` R
Client_ID <- 
Client_Secret <- 
query <- URLencode(iconv("빅데이터","euc-kr","UTF-8"))
contentType = '/json/'
startIndex = '1'
endIndex = '/100/'

url <- paste0('https://openapi.naver.com/v1/search/news?query=',query,
              '&display=100','&start=',1)
doc <- GET(url, add_headers("X-Naver-client-Id" = Client_ID, "X-naver-Client-Secret" = Client_Secret))


json_data <- content(doc, type = 'text', encoding = "UTF-8")
json_obj <- fromJSON(json_data)
navernews <- json_obj$items$title
View(navernews)

navernews <- gsub("</?b>", "", navernews)
navernews <- gsub("&.+t;", "", navernews)

write(text,"navernews.txt")
```

