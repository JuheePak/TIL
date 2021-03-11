### day 15: Groupby

### `1. product_click.log 파일을 읽고 데이터프레임으로 생성하여 다음 질문들을 해결해 본다.`

### `(1) 상품별 클릭수를 바그래프로 그리는데 클릭수가 많은 순으로 그린다.`

``` python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from matplotlib import font_manager, rc
import seaborn as sns

font_path = "./data/210 M고딕030.ttf"
font_name = font_manager.FontProperties(fname=font_path).get_name()
rc('font', family=font_name)

df = pd.read_csv('./data/product_click.log', header=None, sep=' ')
df.columns=['oldclicktime', 'clickpid']
#display(df.head())
df1 = df.groupby('clickpid').count()
df1.sort_values(by='oldclicktime', ascending=False, inplace=True)
#or
#result = clickpid_agg.sort_values(ascending=False, inplace = True)
#display(df1)
mycolors = sns.color_palette('Blues', len(df1['oldclicktime']))

plt.figure(figsize=(10, 10))
plt.ylabel('클릭횟수', size=15)
plt.xlabel('상품 ID', size=15)
plt.title('상품별 클릭 횟수', size=20)
plt.grid(True)
plt.bar(df1.index, df1['oldclicktime'], color=mycolors)
plt.xticks(size=10, rotation='30')

plt.show()
```



### `(2) 어떤 요일에 가장 많이 클릭하는지 다음과 같이 출력하라.`

> 클릭 수가 제일 많은 요일은 목요일입니다.

``` python
df['oldclicktime'] = df['oldclicktime'].astype('str')
df['clicktime'] = pd.to_datetime(df['oldclicktime'])
df['hour'] = df['clicktime'].dt.hour
df.drop('oldclicktime', axis=1, inplace=True)
df['weekdays'] = pd.DatetimeIndex(df['clicktime']).day_name()


df2 = df.groupby('weekdays').count()
df2.sort_values(by='clicktime', ascending=False, inplace=True) #내림차순
df2.reset_index(inplace=True)
#display(df2)
result1 = df2.loc[0, 'weekdays'] # 가장 많은 요일
#print(result1)

print('클릭 수가 제일 많은 요일은 ', result1 ,'입니다.', sep='')
```



### `(3) 어느 시간대에 가장 많이 클릭하는지 다음과 같이 출력하라.`

> 9시와 10시 사이에 제일 많이 클릭했습니다.

``` python
df3 = df.groupby('hour').count()
df3.sort_values(by='clicktime', ascending=False, inplace=True) #내림차순
df3.reset_index(inplace=True)
#display(df3)
result2 = df3.loc[0, 'hour'] # 가장 많은 시간대

print(result2,'시와 ', (result2)+1,'시 사이에 제일 많이 클릭했습니다.', sep='')

# plog = pd.read_pickle("../product_log.pickle") # to_pickle()
# display(plog.head())
```



### `2. 제공된 emp.csv를 읽고 데이터프레임으로 생성하여 다음 질문들을 해결하라.`

### `(1) 부서별 월급의 합`

``` python
df = pd.read_csv('./data/emp.csv', header=0)
# print(df.head())

# 부서 월급의 합
df1 = df[['deptno', 'sal']]
df1= df1.groupby('deptno').sum()
display(df1)
```



### `(2) 직무(job)별 월급의 합`

``` python
# 직무별 월급의 합
df2 = df[['job', 'sal']]
df2 = df2.groupby('job').sum()
display(df2)
```



### `(3) 부서와 직무(job)별 최고 월급과 입사한지 가장 오래된 직원의 입사날짜`

``` python
#부서와 직무(job)별 최고 월급과 입사한지 가장 오래된 직원의 입사날짜
df3 = df.loc[:, ['deptno','job', 'sal', 'hiredate']]
df3['hiredate'] = pd.to_datetime(df3['hiredate'])
df3 = df3.groupby(['deptno', 'job'])
df3 = df3.agg({'sal':'max', 'hiredate':'min'})
display(df3)
```



### `(4) 직무(job)와 부서별 최고 월급`

``` python
# 직무(job)와 부서별 최고 월급
df4 = df[['deptno', 'job', 'sal']]
df4 = df4.groupby(['job', 'deptno']).max('sal')
display(df4)
```

