### day 11: Matplotlib

### `1. matplotlib을 이용하여 아래 데이터를 읽어 가로막대그래프로 시각화하라.`

> 읽어올 데이터 'data/cctv_seoul.csv'

``` python
import pandas as pd
import matplotlib.pyplot as plt
from matplotlib import font_manager, rc
import seaborn as sns
mycolors = sns.color_palette('Greens', len(df['구별']))

#폰트깨짐 해결
font_path = "./data/210 M고딕030.ttf"
font_name = font_manager.FontProperties(fname=font_path).get_name()
rc('font', family=font_name)

#데이터 읽어와서 구, CCTV 정보만 뽑아냄
df = pd.read_csv('data/cctv_seoul.csv', header=0)
#print(df.head())
df1 = df[['구별', 'CCTV수']]
#display(df1)

#그래프 그리기
df1.set_index('구별', inplace=True)
#display(df1)

plt.figure(figsize=(10, 10))
plt.xlabel('각 구에 설치된 CCTV 댓수', size=15)
plt.ylabel('구이름', size=15)
plt.title('시각화 과제(1) 각 구의 CCTV 설치 현황', size=20)
plt.barh(df1.index, df1['CCTV수'], height=1, color=mycolors)
plt.grid(True)


#저장
plt.savefig("output/hw1.png")
```

결과:![hw1](C:\Users\juhee\TIL\Python for Data Analysis\hw1.png)

### `2. matplotlib을 이용하여 아래 데이터를 읽어 세로막대그래프로 시각화하라.`

> 읽어올 데이터: 'data/cctv_seoul.csv'

``` python
import pandas as pd
import matplotlib.pyplot as plt
from matplotlib import font_manager, rc
import seaborn as sns
mycolors = sns.color_palette('Reds', len(df['구별']))

#폰트깨짐 해결
font_path = "./data/210 M고딕030.ttf"
font_name = font_manager.FontProperties(fname=font_path).get_name()
rc('font', family=font_name)

#데이터 읽어와서 구, CCTV 정보만 뽑아냄
df = pd.read_csv('data/cctv_seoul.csv', header=0)
#print(df.head())
df1 = df[['구별', 'CCTV수']]
# CCTV수 기준 내림차순 정렬함
df1.sort_values(by='CCTV수', ascending=False, inplace=True)
#display(df1)

#그래프 그리기
df1.set_index('구별', inplace=True)
#display(df1)
plt.figure(figsize=(10, 10))
plt.ylabel('각 구에 설치된 CCTV 댓수', size=15)
plt.xlabel('구이름', size=15)
plt.title('시각화 과제(2) 각 구의 CCTV 설치 현황', size=20)
plt.grid(True)
plt.bar(df1.index, df1['CCTV수'], color=mycolors)

#y축 회전
plt.xticks(size=10, rotation='vertical')

#저장
plt.savefig("output/hw2.png")
```

결과:

![hw2](C:\Users\juhee\TIL\Python for Data Analysis\hw2.png)

