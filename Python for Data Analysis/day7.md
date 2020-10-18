### day 7: Selenium

### `해당 웹사이트에서 2+1 행사를 진행하는 품목의 이름과 가격을 첫 페이지부터 마지막 페이지까지 스크래핑하여 저장한다. 단, 가격 정보의 '원'과 천단위를 구분하는 콤마(,)를 제거하여 gs25_twotoone.csv로 저장한다.`

``` python
from selenium import webdriver
import re

driver = webdriver.Chrome('C:/Temp/chromedriver')
driver.implicitly_wait(3) 

driver.get('http://gs25.gsretail.com/gscvs/ko/products/event-goods')
import time
time.sleep(2)
go_twotoone = driver.find_element_by_id('TWO_TO_ONE')
go_twotoone.click()
time.sleep(1)

name = []
price = []
    
for k in range(93):
    n = driver.find_elements_by_css_selector('div.prod_box > p.tit')
    p = driver.find_elements_by_css_selector('div.prod_box > p.price > span.cost')
     
    for i in n:
        name.append(i.text)
        goodsname = ' '.join(name).split()

    for k in p:
        content = k.text.strip()
        content = re.sub(',', '', content)
        content = re.sub('원', '', content)
        content = re.sub('[\n\t]', '', content)
        price.append(content)
        goodsprice = ' '.join(price).split()
             
    next_url = 'div.cnt > div.cnt_section.mt50 > div > div > div:nth-child(5) > div > a.next'
    next_page = driver.find_element_by_css_selector(next_url)
    next_page.click()
    time.sleep(3)
    

print(goodsname)
print(goodsprice)

with open('gs25_twotoone.csv', "wt", encoding="utf-8") as f:
    f.write('goodsname,goodsprice\n')  
    for i in range(len(goodsprice)):
        f.write(goodsname[i]+','+goodsprice[i]+'\n')  

time.sleep(2)
driver.quit()
```

