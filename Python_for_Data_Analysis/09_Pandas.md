### day 9: Pandas

### `1. 다음에 제시된 소스로 Series를 생성하고 blood를 인덱스로 하는 dataframe을 구현하라`

```python
# pandas 불러오기 
import pandas as pd
print("pandas version: ", pd.__version__)

blood = ['A형', 'B형', 'O형', 'AB형']
st = [34.2, 27.1, 26.7, 11.5]
sr = pd.Series(st, index=blood)
print(sr)
```



### `2. 다음에 제시된 내용으로 DataFrame 을 생성하고 서브 문제에서 제시된 기능을 구현하라.`

``` python
data = {
    'name':['듀크1', '듀크2', '듀크3', '듀크4', '듀크5', '듀크6', '듀크7'],
    'kor':[90, 80, 70, 70, 60, 70, 90],
    'eng':[99, 98, 97, 46, 77, 56, 90],
    'mat':[90, 70, 70, 60, 88, 99, 90],
}
df = pd.DataFrame(data)                      
```

### `앞, 뒤에서 다섯 행만 출력하라.`

``` python
# 앞
print(df.iloc[0:5])
# OR
print(df.head())
# 뒤
print(df.iloc[2:])
# OR
print(df.tail())
```

### `칼럼명을 출력한다.`

### `name 칼럼만 출력한다. (추출시 [] 사용)`

### `eng 칼럼만 출력한다. (추출시 . 사용)`

### `kor과 mat 칼럼만 출력한다`.

``` python
# 전체 칼럼명
print(df.columns)
# name 칼럼만 
print(df['name'])
# eng 칼럼만
print(df.eng)
# kor 과 mat 칼럼만
print(df[['kor', 'mat']])
```

### `iloc 인덱서를 사용하여 네 번째 행을 출력한다.`

### `iloc 인덱서를 사용하여 첫 번째 행, 첫 번째 열을 출력한다.`

### `iloc 인덱서를 사용하여 네 번째 행, 세 번째 열을 출력한다.`

### `iloc 인덱서를 사용하여 세 번째와 네 번째 행의 세 번째 열을 출력한다.`

### `iloc 인덱서를 사용하여 세 번째와 네 번째 행의 세 번째와 네 번째열을 출력한다.`

```python
# 네번째행 출력
print(df.iloc[[3]])
# 첫번째행, 첫번째 열
print(df.iloc[0,0])
# 네번째행, 세번째열
print(df.iloc[3,2]) #4x3
#세번째와 네번째 행의 세번째열
print(df.iloc[2:4, 2:3])
# 세번째 네번째행의 세번째 네번째열
print(df.iloc[2:4, 2:4])
```



### `loc 인덱서를 사용하여 네 번째 행을 출력한다.`

### `loc 인덱서를 사용하여 첫 번째 행, 첫 번째 열을 출력한다.`

### `loc 인덱서를 사용하여 네 번째 행, 세 번째 열을 출력한다.`

### `loc 인덱서를 사용하여 세 번째와 네 번째 행의 세 번째 열을 출력한다.`

### `loc 인덱서를 사용하여 세 번째와 네 번째 행의 세 번째와 네 번째열을 출력한다.`

``` python
# 네번째행
print(df.loc[3])
# 첫번째행 첫번째열
print(df.loc[0,['name']])
# 네번째행 세번째열
print(df.loc[3,['eng']])
# 세번째 네번째행의 세번째열
print(df.loc[2, ['mat']])
# 세번째와 네번째행의 세번째와 네번째열
print(df.loc[2:3, ['eng', 'mat']])
```



### `3. 위의 문제에서 사용한 df 라는 DataFrame의 숫자 index를 name 컬럼으로 변경하고 df 를 출력한다.`

``` python
print(df)
df.set_index('name', inplace = True)
print(df)
```

