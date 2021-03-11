### day 6: Selenium



### `아래 제공된 페이지(신라스테이 역삼)의 모든 댓글을 추출하는 기능을 동적 크롤링으로 구현하고 naverhotel.txt로 저장하라.`

> [https://hotel.naver.com/hotels/item?hotelId=hotel:Shilla_Stay_Yeoksam&destination_kor=%EC%8B%A0%EB%9D%BC%EC%8A%A4%ED%85%8C%EC%9D%B4%20%EC%97%AD%EC%82%BC&rooms=2](https://hotel.naver.com/hotels/item?hotelId=hotel:Shilla_Stay_Yeoksam&destination_kor=신라스테이 역삼&rooms=2)



### Case1: 댓글리뷰가 총 10페이지임을 알고 활용한다.

``` python
from selenium import webdriver

driver = webdriver.Chrome('C:/Temp/chromedriver')
driver.implicitly_wait(3) 

driver.get("https://hotel.naver.com/hotels/item?hotelId=hotel:Shilla_Stay_Yeoksam&destination_kor=%EC%8B%A0%EB%9D%BC%EC%8A%A4%ED%85%8C%EC%9D%B4%20%EC%97%AD%EC%82%BC&rooms=2")
import time
time.sleep(2)

mylist =[]
page = []


while True:
    reviews = driver.find_elements_by_class_name('review_desc') #리뷰
    for r in reviews:
        mylist.append(r.text)
        
    next_page = driver.find_elements_by_css_selector('div.content > div.hotel_used_review.ng-isolate-scope > div.review_ta.ng-scope > div.paginate > a.direction.next')
    for p in next_page:
        page.append(p.text)
    
    if len(page) == 10 : #활성화된 다음 페이지의 버튼 개수를 세서, 총 10개(10페이지)가 될 경우 멈춘다.
        break
        
    go_next = 'div.content > div.hotel_used_review.ng-isolate-scope > div.review_ta.ng-scope > div.paginate > a.direction.next'
    next_link = driver.find_element_by_css_selector(go_next)
    next_link.click()   
    time.sleep(3)

        
wfile = open("naverhotel_1.txt","w", encoding="utf-8") 
wfile.writelines(mylist) 
wfile.close()
```



### Case2: a.direction.next.disabled를 활용한다.

``` python
from selenium import webdriver

driver = webdriver.Chrome('C:/Temp/chromedriver')
driver.implicitly_wait(3) 

driver.get("https://hotel.naver.com/hotels/item?hotelId=hotel:Shilla_Stay_Yeoksam&destination_kor=%EC%8B%A0%EB%9D%BC%EC%8A%A4%ED%85%8C%EC%9D%B4%20%EC%97%AD%EC%82%BC&rooms=2")
import time
time.sleep(2)

mylist =[]
page = []


while True:
    reviews = driver.find_elements_by_class_name('review_desc') #리뷰
    for r in reviews:
        mylist.append(r.text)
        
    next_page = driver.find_elements_by_css_selector('div.content > div.hotel_used_review.ng-isolate-scope > div.review_ta.ng-scope > div.paginate > a.direction.next.disabled')
    for p in next_page:
        page.append(p.text)
    
    if len(page) == 1: #다음 버튼이 비활성화 될 경우 멈춘다.
        break
        
    go_next = 'div.content > div.hotel_used_review.ng-isolate-scope > div.review_ta.ng-scope > div.paginate > a.direction.next'
    next_link = driver.find_element_by_css_selector(go_next)
    next_link.click()   
    time.sleep(3)

        
wfile = open("naverhotel_2.txt","w", encoding="utf-8") 
wfile.writelines(mylist) 
wfile.close()

driver.quit()
```



