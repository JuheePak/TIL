### day4: Scraping

### `다음의 영화 <밥정>의 리뷰와 평점을 모두 스크래핑하여 csv파일로 저장하라.`

### `단, 마지막 페이지가 5페이지라는 것을 모른다고 가정하고 코드를 구현하라.`

``` python
import requests
from bs4 import BeautifulSoup
import re

movie_reviews = []
movie_grades = []
cnt = 0

urlstr = 'https://movie.daum.net/moviedb/grade?movieId=131704&type=netizen'
r = requests.get(urlstr)
r.encoding = 'utf-8'
bs = BeautifulSoup(r.text, 'html5lib') #파서를 html5lib으로 변경
page = bs.select('.inner_paging > .link_page') #페이지 수를 확인할 수 있는 셀렉터

for i in page:
    page = i.string #그 중 가장마지막 page
#print(page) #5 

for m in range(5):
    m += 1
    urlstr = 'https://movie.daum.net/moviedb/grade?movieId=131704&type=netizen'
    p = '&page='
    myurl = urlstr+p+str(m)
    r = requests.get(myurl)
    r.encoding = 'utf-8'
    bs = BeautifulSoup(r.text, 'html.parser')
    
    grades = bs.select('.emph_grade') #평점
    reviews = bs.select('.desc_review') #리뷰
    
    for i in reviews:
        movie_reviews.append(i.text.strip())
        
    for k in grades:
        movie_grades.append(k.string)
        
print('----리뷰점수-------')      
print(movie_grades)
print('----영화리뷰-------')
print(movie_reviews)

with open('bj.csv', "wt", encoding="utf-8") as f:
    f.write('movie_grades,movie_reviews\n')  
    for i in range(len(movie_grades)):
        f.write(movie_grades[i]+', '+movie_reviews[i]+'\n')  
```

### OR

```python
import requests
from bs4 import BeautifulSoup
import re
n = 1

while True:
    req = requests.get('https://movie.daum.net/moviedb/grade?movieId=131704&type=netizen&page='+str(n))
    html = req.text
    soup = BeautifulSoup(html, 'html5lib')
    points = soup.select('div.raking_grade > em')
    reviews = soup.select('div.main_detail > ul > li > div > p')
    if len(points) == 0 :
        break

    movie_point = []
    movie_review = [] 

    for dom in points:
        movie_point.append(dom.text)

    for dom in reviews:
        content=dom.text.strip()
        content=re.sub("[\n\t]", ' ', content)
        movie_review.append(content)

        
    commentLength = len(movie_point)   
    for i in range(commentLength):
        print(movie_point[i] + ","+movie_review[i]) 
    n += 1
```

