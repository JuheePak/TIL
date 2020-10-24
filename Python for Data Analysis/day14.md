### day 14: Missing Data

### `1. 다음에 제시된 코드를 수행시켜서 누락데이터를 일부 갖게되는 데이터 프레임을 생성한다.`

``` python
import pandas as pd
import seaborn as sns
import numpy as np
iris = sns.load_dataset("iris")
iris_x = iris.loc[:,['sepal_length', 'sepal_width',
            'petal_length', 'petal_width']]
import random
random.seed(1)
for col in range(4):
    iris_x.iloc[[random.sample(range(len(iris)), 20)], col] = float('nan')
iris_x.head(10)
```

### `NaN 값이 어떤 행/렬에 포함되지 않도록 누락데이터를 처리하시오. `

``` python
print('1-1')
new_iris_x = iris_x.dropna()
display(new_iris_x.head(3))
```



### `2. 행을 기준으로 NaN이 2개 이상인 행을 제거하여 출력하시오.`

``` python
print('1-2')
one_na_iris_x = iris_x.dropna(subset=['sepal_length', 'sepal_width', 'petal_width'], axis=0, how='all')
display(one_na_iris_x.head(10))
```



### `3. 'sepal_length', 'sepal_width' 열 기준 NaN값이 한개라도 포함되어 있는 행을 제거하시오.`

```python
print('1-3')
one_na_iris_x = iris_x.dropna(subset=['sepal_length', 'sepal_width'], axis=0, how='any')
display(one_na_iris_x.head(10))
```



### `4. NaN 값을 0으로 치환하라.`

``` python
print('1-4')
num = 0
df = iris_x.copy()
df['sepal_length'].fillna(num, inplace=True)
df['sepal_width'].fillna(num, inplace=True)
df['petal_length'].fillna(num, inplace=True)
df['petal_width'].fillna(num, inplace=True)
display(df.head(10))
```



### `5. NaN 값을 평균으로 치환하라.`

``` python
print('1-5')
df1 = iris_x.copy()
mean_se_len = round(iris_x['sepal_length'].mean(axis=0), 1)
mean_se_wid = round(iris_x['sepal_width'].mean(axis=0), 1)
mean_pe_len = round(iris_x['petal_length'].mean(axis=0), 1)
mean_pe_wid = round(iris_x['petal_width'].mean(axis=0), 1)
df1['sepal_length'].fillna(mean_se_len, inplace=True)
df1['sepal_width'].fillna(mean_se_wid, inplace=True)
df1['petal_length'].fillna(mean_pe_len, inplace=True)
df1['petal_width'].fillna(mean_pe_wid, inplace=True)
display(df1.head(10))
```



### `6. NaN 값을 10으로 치환하라.`

``` python
print('1-6')
num = 10
df2 = iris_x.copy()
df2['sepal_length'].fillna(num, inplace=True)
df2['sepal_width'].fillna(num, inplace=True)
df2['petal_length'].fillna(num, inplace=True)
df2['petal_width'].fillna(num, inplace=True)
display(df2.head(10))
```



### `7. NaN 값을 직전 행의 값으로 치환하라.`

``` python
print('1-7')
df3 = iris_x.copy()
df3['sepal_length'].fillna(method = 'ffill', inplace=True)
df3['sepal_width'].fillna(method = 'ffill', inplace=True)
df3['petal_length'].fillna(method = 'ffill', inplace=True)
df3['petal_width'].fillna(method = 'ffill', inplace=True)
display(df3.head(10))
```

