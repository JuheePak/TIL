### day 8: Social Media Open API

### `네이버 지역 서비스에 등록된 각 지역별 업체 및 상호 검색에서 '쌀국수'집 5개를 검색해서 출력하는 코드를 작성하며 XML 형식 응답 요청과 JSON 형식 응답 요청을 각각의 셀에 구현하라.`

> https://openapi.naver.com/v1/search/local.xml
>
> https://openapi.naver.com/v1/search/local.json



### XML 형식의 응답 요청

```python
from bs4 import BeautifulSoup
import urllib.request as req
import io

num = 5
query = '쌀국수'
encText = urllib.parse.quote_plus(query)
client_key = 
client_secret = 

url = 'https://openapi.naver.com/v1/search/local.xml?query=' + encText + '&display=' + str(num)+'/'
request = urllib.request.Request(url)
request.add_header("X-Naver-Client-Id",client_key)
request.add_header("X-Naver-Client-Secret",client_secret)

response = urllib.request.urlopen(request)
rescode = response.getcode()
if(rescode == 200):
    response_body = response.read()
    xml = response_body.decode('utf-8')
    soup = BeautifulSoup(xml, 'xml')
    #print(xml)
    
    pholist = []
    for p in soup.find_all('item') :
        title = p.find('title').string
        title = '없음' if title is None else title
        address = p.find('address').string
        address = '없음' if address is None else address
        pholist.append((title, address))
    count = 1
    print('['+ query + '집에 대한 네이버 지역 정보(XML)]')
    for title, address in pholist :
        print(str(count) + ' : ' + title +','+ address, sep='')
        count += 1
    
else:
    print("Error code:"+rescode)
```



### JSON 형식의 응답 요청

``` python
import urllib.request
import json

client_key = ''
client_secret = ''

query = '쌀국수'
encText = urllib.parse.quote_plus(query)

num = 5
naver_url = 'https://openapi.naver.com/v1/search/local.json?query=' + encText + '&display=' + str(num)
request = urllib.request.Request(naver_url)
request.add_header("X-Naver-Client-Id",client_key)
request.add_header("X-Naver-Client-Secret",client_secret)
response = urllib.request.urlopen(request) 

rescode = response.getcode()

if(rescode == 200):
    response_body = response.read()
    dataList = json.loads(response_body)
    count = 1
    print('['+ query + '집에 대한 네이버 지역 정보(JSON)]')
    for data in dataList['items'] :
        print (str(count) + ' : ' + data['title']+','+data['address'])
        count += 1
else:
    print('오류 코드 : ' + rescode)
```

