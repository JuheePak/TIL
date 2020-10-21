### day 10: Read, save dataframe

### `1. (1) "./data/score.csv"파일을 읽고 칼럼명, 인덱스, dataframe을 출력해 본다.`

``` python
import pandas as pd

file_path = "./data/score.csv"
df1 = pd.read_csv(file_path)
print('칼럼명: ', df1.columns)
print('인덱스: ', df1.index)
display(df1)
```



### `2. "./data/score_noheader.csv"파일을 읽고, 칼럼명과 인덱스를 출력한다. 단, 칼럼명을 영어로 수정하며 각 행의 합인 total과 평균인 avg를 추가한다.`

``` python
file_path = "./data/score_noheader.csv"
df2 = pd.read_csv(file_path, header=None)
display(df2)
print('칼럼명: ', df2.columns)
print('인덱스: ', df2.index)
print('칼럼명추가------------')
df2.columns=['name', 'kor', 'eng', 'mat']
print('칼럼명: ', df2.columns)
display(df2)
print('total과 avg열 추가------------')
df2['total'] = df2['kor']+df2['eng']+df2['mat']
df2['avg'] = df2['total']/3
display(df2)
```



### `3. "data/mydata.json" 파일을 읽고 앞에서부터 5개 행, 뒤에서부터 5개 행, 앞에서부터 10개의 행, 전체 (행,열)의 개수를 출력한다.`

``` python
file_path = "./data/mydata.json" 
df = pd.read_json(file_path)
print('[기본정보보기]')
print(df.info())
print('앞에서 부터 5개만 미리 보기')
print(df.head())
print('뒤에서 부터 5개만 미리 보기')
print(df.tail())
print('앞에서 부터 10개만 미리 보기')
print(df.head(10))
print(df.shape)
print('행의 개수: ',df.shape[0],'열의 개수',df.shape[1])
```



### `4. "./data/mpgdata.csv" 파일을 읽고 앞에서부터 3개의 행, 전체 (행, 열)의 개수와 행의 개수, 열의 개수를 각각 출력하고 데이터프레임의 요약 정보를 출력하라. `

``` python
file_path = "./data/mpgdata.csv"
df = pd.read_csv(file_path)
print('앞에서 부터 3개만 미리 보기')
display(df.head(3))
print(df.shape)
print('행의 개수: ',df.shape[0])
print('열의 개수', df.shape[1])
print('기술통계 정보 요약')
display(df.describe())
```

