## day 13: 동적크롤링

### `1. gs25 사이트에서 2+1 행사를 진행하는 모든 상품들의 상품명과 가격을 추출하여 데이터 프레임으로 생성한 다음 gs25_twotoone.csv 에 저장하는 R 코드를 작성하시오.`

> **가격은 콤마와 원을 제외한 숫자만 저장**
>
> **상품명의 변수명은 goodsname, 가격의 변수명은 goodsprice 가 되도록 한다.**
>
> **http://gs25.gsretail.com/gscvs/ko/products/event-goods**

``` R
library(RSelenium)
remDr <- remoteDriver(remoteServerAddr = "localhost" , port = 4445, browserName = "chrome")
remDr$open()

url <- "http://gs25.gsretail.com/gscvs/ko/products/event-goods"
remDr$navigate(url)

# 2+1페이지로 넘어가기
pageLink <- remDr$findElements(using='css', '#TWO_TO_ONE')
remDr$executeScript("arguments[0].click();", pageLink)
Sys.sleep(2)

# 가장 끝 페이지로 넘어가서 마지막 페이지 찾기.
endPage <- remDr$findElements(using='css', "div.paging > a.next2")
remDr$executeScript("arguments[0].click();", endPage)
Sys.sleep(2)
findendPage <- remDr$findElement(using='css', "div:nth-child(5) > div > span > a.on")
mypage <- findendPage$getElementText() # 마지막 페이지는 102.
mypage <- as.numeric(mypage)

# 다시 첫 페이지로 돌아오기
pageLink <- remDr$findElements(using='css', '#TWO_TO_ONE')
remDr$executeScript("arguments[0].click();", pageLink)
Sys.sleep(2)

goodsname <- NULL; goodsprice <- NULL; nextPage <- NULL

repeat{
  namenodes <- remDr$findElements(using='css', 'div.prod_box > p.tit')
  Sys.sleep(1)
  mygoodsname <- sapply(namenodes, function(x) {x$getElementText()})
  mygoodsname <- mygoodsname[nchar(mygoodsname) > 0]
  
  goodsname <- append(goodsname, unlist(mygoodsname))
  
  pricenodes <- remDr$findElements(using='css', 'div.prod_box > p.price > span.cost')
  Sys.sleep(1)
  mygoodsprice <- sapply(pricenodes, function(x) {x$getElementText()})
  mygoodsprice <- mygoodsprice[nchar(mygoodsprice) > 0]
  mygoodsprice <- gsub("[^[:digit:]]", "", mygoodsprice)

  goodsprice <- append(goodsprice, unlist(mygoodsprice))
  
  findendPage <- remDr$findElement(using='css', "div:nth-child(5) > div > span > a.on")
  lastpage <- findendPage$getElementText()
  lastpage <- as.numeric(lastpage)
  
  if (mypage == lastpage)
    break
  
  cat(length(goodsname)/8, "페이지 \n")
  nextPage <- remDr$findElements(using='css',"div.paging > a.next")
  remDr$executeScript("arguments[0].click();", nextPage)
  Sys.sleep(1)
  
}


df <- data.frame(goodsname, goodsprice)
write.table(df,"gs25_twotoone.csv")

```

