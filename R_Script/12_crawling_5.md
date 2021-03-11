## day 12:  동적크롤링

### `1. 다음 사이트(네이버 호텔 페이지에서 신라스테이 역삼에 대한 페이지)의 모든 댓글(리뷰)들을 추출하는 기능을 동적 크롤링으로 구현해 본다.`

> [https://hotel.naver.com/hotels/item?hotelId=hotel:Shilla_Stay_Yeoksam&destination_kor=%EC%8B%A0%EB%9D%BC%EC%8A%A4%ED%85%8C%EC%9D%B4%20%EC%97%AD%EC%82%BC&rooms=2](https://hotel.naver.com/hotels/item?hotelId=hotel:Shilla_Stay_Yeoksam&destination_kor=신라스테이 역삼&rooms=2)

``` R
library(RSelenium)
remDr <- remoteDriver(remoteServerAddr = "localhost" , port = 4445, browserName = "chrome")
remDr$open()
remDr$navigate("http://www.google.com/")

url<-'https://hotel.naver.com/hotels/item?hotelId=hotel:Shilla_Stay_Yeoksam&destination_kor=%EC%8B%A0%EB%9D%BC%EC%8A%A4%ED%85%8C%EC%9D%B4%20%EC%97%AD%EC%82%BC&rooms=2'
remDr$navigate(url)
Sys.sleep(3)
pageLink <- NULL
noNext <- NULL
reple <- NULL

repeat{
  doms <- remDr$findElements(using = "css", ".review_desc")
  Sys.sleep(1)
  reple_v <- sapply(doms, function (x) {x$getElementText()})
  print(reple_v)
  reple <- append(reple, unlist(reple_v))
  cat(length(reple)/4, "페이지 \n")
  pageLink <- remDr$findElements(using='css',"div.ng-scope > div.container.ng-scope > div.content > div.hotel_used_review.ng-isolate-scope > div.review_ta.ng-scope > div.paginate > a.direction.next")
  remDr$executeScript("arguments[0].click();", pageLink)
  Sys.sleep(2)
  
  noNext <- remDr$findElements(using='css', "a.direction.next.disabled")
  if (length(noNext) == 1)  { 
    # 다음버튼이 비활성화되었을때(10p)의 클래스 네임은 a.direction.next.disabled임을 활용하였음.
    # 마지막 페이지까지 크롤링 후, break로 repeat를 멈춘다.
    
    doms <- remDr$findElements(using = "css", ".review_desc")
    Sys.sleep(1)
    reple_v <- sapply(doms, function (x) {x$getElementText()})
    print(reple_v)
    reple <- append(reple, unlist(reple_v))
    cat(length(reple)/4, "페이지 \n")
    cat("마지막 페이지로 크롤링 종료\n")
    break
  }
}
cat(length(reple), "개의 댓글 추출\n")

write(reple,"naverhotel_2.txt")

```

