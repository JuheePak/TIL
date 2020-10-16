### day2: Scraping

### `다음에 제시된 URL 문자열로 요청되는 페이지의 내용에서 요구되는 태그의 내용과 속성을 출력해 본다.`

> **<h1> 태그의 콘텐츠**
>
> **텍스트 형식으로 내용을 가지고 있는 <a> 태그의 콘텐츠와 href 속성값**
>
> **<img> 태그의 src 속성값**
>
> **첫 번째 <h2> 태그의 콘텐츠**
>
> **<ul> 태그의 자식 태그들 중 style 속성의 값이 green으로 끝나는 태그의 콘텐츠**
>
> **두 번째 <h2> 태그의 콘텐츠**
>
> **[<ul> 태그의 모든 자식 태그들의 콘텐츠** 
>
> <table> 태그의 모든 자손 태그들의 콘텐츠 
>
> **name이라는 클래스 속성을 갖는 <tr> 태그의 콘텐츠**
>
> **target이라는 아이디 속성을 갖는 <td> 태그의 콘텐츠**



``` python
import requests
import re
from bs4 import BeautifulSoup

req = requests.get('') #강사님이 제공해주신 주소 생략
html = req.content
html = html.decode('utf-8')
bs = BeautifulSoup(html, 'html.parser')

print("[<h1>태그의 컨텐트]", bs.h1.text)
print("[텍스트 형식으로 내용을 가지고 있는 <a>태그의 컨텐트와 href 속성값]")
print(bs.find_all('a')[0].text, ': ', bs.a['href'], sep='')
print(bs.find_all('a')[1].text, ': ', bs.find_all('a')[1].attrs, sep='')
print(bs.find_all('a')[2].text, ': ', bs.find_all('a')[2].attrs, sep='')
#OR
aTag = bs.find_all('a')
for tag in aTag:
    if(tag.text.strip()):
        print(tag.text, ': ', tag['href'], sep='')
print("<img>태그의 src 속성값: ", bs.img['src'], sep='')
print("첫번째 <h2> 태그의 컨텐트: ", bs.find('h2').text, sep='')
print("<ul> 태그의 자식 태그들중 style 속성의 값이 green으로 끝나는 태그의 컨텐트: ", bs.find_all('li')[2].text, sep='')
print("<ul> 태그의 자식 태그들중 style 속성의 값이 green으로 끝나는 태그의 컨텐트: ", bs.ul.find(style=re.compile("green$")).text, sep='')
print("두 번째 <h2> 태그의 콘텐츠: ", bs.find_all('h2')[1].text, sep='')
print("<ol> 태그의 모든 자식 태그들의 컨텐트: ", bs.ol.text.strip(), sep='')
#OR
olTag =bs.find('ol')
olliTag = olTag.find_all("li")
for tag in olliTag:
    print(tag.text)
#OR
for tg in bs.find('ol').find_all('li'):
    print(tg.text)    
print("<table> 태그의 모든 자손 태그들의 컨텐트: ", bs.table.text.strip(), sep='')
print("name 이라는 클래스 속성을 갖는 <tr> 태그의 컨텐트: ", bs.find('tr', class_="name").text, sep='')
print("target이라는 아이디 속성을 갖는 <td> 태그의 컨텐트: ", bs.find("td", id='target').text, sep='')
```

### 출력물

![image-20201015131348526](C:\Users\juhee\TIL\Python for Data Analysis\image-20201015131348526.png)

