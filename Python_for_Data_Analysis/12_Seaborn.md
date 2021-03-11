### day 12: Seaborn

### `제시된 cctv_seoul.csv 파일 내용을 읽어 아래 조건과 같이 전처리 한 후 시각화하여 출력하라.`

> 인구수 대비 CCTV수와 인구수 대비 고령자 비율을 계산하여 각각 CCTV비율과 노인비율이라는 열을 추가하라.
>
> 인덱스를 '구별'로 설정한다.



```python
import pandas as pd
import matplotlib.pyplot as plt
from matplotlib import font_manager, rc
import seaborn as sns

#폰트깨짐 해결
font_path = "./data/210 M고딕030.ttf"
font_name = font_manager.FontProperties(fname=font_path).get_name()
rc('font', family=font_name)

df = pd.read_csv('data/cctv_seoul.csv', header=0)
df.set_index('구별', inplace=True)
df['CCTV비율'] = df['CCTV수']/df['인구수'] * 100
df['고령자비율'] = df['고령자']/df['인구수'] * 100
print('[전처리 결과]')
display(df.head())

print('[시각화 결과]')
# 그래프 객체 생성 (figure에 2개의 서브 플롯을 생성)
fig = plt.figure(figsize=(18, 10))   
ax1 = fig.add_subplot(2, 1, 1)
ax2 = fig.add_subplot(2, 1, 2)

# 그래프 그리기 - bar
sns.barplot(x=df.index,        #x축 변수
            y=df['CCTV비율'],       #y축 변수
            data=df,   #데이터
            ax=ax1).set_title('각 구의 인구수 대비 CCTV 비율', fontsize=20)         #axe 객체 - 1번째 그래프
ax1.set(xlabel=None, ylabel='CCTV 비율')

# 그래프 그리기 - line-scatter
sns.scatterplot(x=df.index,        #x축 변수
            y=df['고령자비율'],        #y축 변수
            data=df,   #데이터
            color='olive',
            ax=ax2).set_title('각 구의 인구수 대비 고령자 비율', fontsize=20)
ax2.set(xlabel=None, ylabel='노인비율')

sns.lineplot(x=df.index,        #x축 변수
            y=df['고령자비율'],        #y축 변수
            data=df,   #데이터
            color='y',
            ax=ax2)
ax2.set(xlabel=None, ylabel='노인비율')

#저장
plt.savefig("output/hw3.png")

plt.show()
```

