### day 5: Selenium

### `selenium을 이용하여 크롬브라우저를 기동시키고 네이버 홈페이지에서 파이썬이라는 검색어를 전달하여 검색을 요청하는 과정을 구현한다. 검색어를 입력하는 검색어 입력상자의 Webelement 객체를 찾아야 하는데 아래 제시된 3가지의 방법을 모두 구현한다. `



### `1. CSS 선택자 사용`

```python
from selenium import webdriver
from selenium.webdriver.common.keys import Keys 

driver = webdriver.Chrome('C:/Temp/chromedriver')
driver.get('http://www.naver.com/') 
target=driver.find_element_by_css_selector("[name = 'query']")
target.send_keys('파이썬')
target.send_keys(Keys.ENTER)
```



### `2. id 속성 사용 `

``` py
from selenium import webdriver
from selenium.webdriver.common.keys import Keys 

driver = webdriver.Chrome('C:/Temp/chromedriver')
driver.get('http://www.naver.com/') 
target=driver.find_element_by_id('query')
target.send_keys('파이썬')
target.send_keys(Keys.ENTER)
```



### `3. class 속성 사용`

``` python
from selenium import webdriver
from selenium.webdriver.common.keys import Keys 

driver = webdriver.Chrome('C:/Temp/chromedriver')
driver.get('http://www.naver.com/') 
target = driver.find_element_by_class_name('input_text')
target.send_keys('파이썬')
target.send_keys(Keys.ENTER)
```

