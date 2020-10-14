## day1: basic packages

### `파이썬 기반의 정적 수집 실습(1)`

### 첫 번째 셀에는 urllib 패키지를 이용해서 구현하고, 두 번째 셀에는 requests 패키지를 이용하여 구현한다.

### 모든 코드는 Anaconda의 jupyter lab을 이용하여 구현한다.



### `urllib 패키지`

```python
import urllib.request
import urllib.parse
params = urllib.parse.urlencode({'category': '역사', 'page': 25})
url = "" % params # 강사님 웹사이트 주소는 생략
with urllib.request.urlopen(url) as f:
    print(f.read().decode('utf-8'))
```



### `requests 패키지`

``` python
import requests
r = requests.request('get', '', #웹사이트 주소 생략
                     params= {'category':'여행', 'page' : 100})
r.encoding = 'utf-8'
if r.text :
    print(r.text)
else :
    print('응답된 콘텐츠가 없어요')
```

