### day 16: Wordcloud

### `이전에 생성한 naverhotel.txt 파일의 내용을 읽고 형태소 분석을 통해 명사만 추출한 다음, 많이 등장한 순으로 워드클라우드를 처리하고 이미지 파일에 저장하여 제출한다.`

> 백그라운드 칼라는 흰색과 검은색중에 선택한다.
>
> 텍스트 칼라는 팔레트 중에서 선정한다.
>
> 생성되는 이미지의 사이즈는 700*500 이다.
>
> 형태소 분석기 사용은 임의대로 정한다.

``` python
from konlpy.tag import Komoran
from collections import Counter
from PIL import Image   
from wordcloud import WordCloud 
import pandas as pd
import numpy as np 

file = open("./day3/naverhotel_2.txt", 'r', encoding="utf-8") 
lists = file.read()
#print(lists)

komoran = Komoran()
nouns = komoran.nouns(lists)
count = Counter(nouns)
print(count)
```

``` python
del(count['레'])
del(count['잇'])
del(count['전'])
del(count['호텔'])
del(count['으'])
del(count['곳'])
del(count['것'])
del(count['니다'])
del(count['거'])
del(count['수'])
del(count['번'])
del(count['때'])
del(count['탁'])
del(count['갑'])
del(count['호텔']) # 룸이라는 키워드도 한 단어이기 때문에, len()>1 쓰지 않고 하나씩 지워줌
```

``` python
wordcloud = WordCloud(
    stopwords = stopwords,  
    font_path = myfontpath,
    background_color = 'black',
    colormap = 'Accent_r',
    width = 700,
    height = 500
)
```

```python
wordcloud = wordcloud.generate_from_frequencies(count)   
wordcloud.to_file('python_hw.png')

fig = plt.figure()
plt.imshow(wordcloud)
plt.axis('off')
plt.show()
```
![python_hw](https://user-images.githubusercontent.com/69948723/97535551-269b5100-19ff-11eb-9ee6-501c25d76af0.png)
