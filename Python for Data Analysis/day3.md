### day3: Scraping

### `아래의 웹 페이지는 많이 본 순서대로 정렬된 다음 뉴스 페이지이다. 각 뉴스의 타이틀과 신문사명(각 50개)를 스크래핑하여 newstitle, newscomname으로 구성된 news.csv 파일을 생성하라.`

### 단, pandas 말고 with~as로 저장하고, 콤마(,)로 구분되게 하라.

> http://media.daum.net/ranking/popular/

``` python
import requests
from bs4 import BeautifulSoup
import re

title=[]
name=[]

urlstr = 'http://media.daum.net/ranking/popular/'
r = requests.get(urlstr)
r.encoding = 'utf-8'
bs = BeautifulSoup(r.text, 'html.parser')

titleList = bs.select('.rank_news > ul > li > div.cont_thumb > strong > a')
nameList = bs.select('.rank_news > ul > li > div.cont_thumb > strong > span')

for titleDom in titleList:
    title.append(titleDom.string)
for nameDom in nameList:
    name.append(nameDom.string)
    
print(title)
print(name)


with open('news.csv', "wt", encoding="utf-8") as f:
    f.write('newstitle,newscomname\n')  
    for i in range(len(title)):
        f.write('"'+title[i]+'",'+name[i]+'\n')  
```



