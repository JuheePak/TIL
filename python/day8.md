# day 8: List 이해하기

### `1. 비어있는 리스트를 하나 만들고 이 안에 1 ~ 45 사이의 난수를 추출하여 6개를 저장하라. 단, 숫자가 중복되지 않도록 저장한다. 결과는 아래와 같다.`

> **행운의 로또번호: X, X, X, X, X, X**

``` python
import random

lotto = []
cnt = 0
chrTemp = ''

while True:
    if cnt == 6:
        break
    lottoNum = random.randint(1, 45)
    if lottoNum not in lotto:
        cnt += 1
        lotto.append(lottoNum)
        
print('행운의 로또번호 : ', end='')

for lottoNum in lotto:
    chrTemp += str(lottoNum)+','
    
print(chrTemp[0:-2]) # 마지막에 콤마 떼내는 작업

```

### `2. 아래와 같이 구성된 2차원 리스트를 생성하고 아래 소문제와 같은 결과를 출력한다.`

> **10, 12, 14, 16**
>
> **18, 20, 22, 24**
>
> **26, 28, 30, 32**
>
> **34, 36, 38, 40**

### (1) 1행 1열의 데이터: 10

### (2) 3행 4열의 데이터: 32

### (3) 행의 개수: 4

### (4) 열의 개수: 4

### (5) 3행의 데이터들: 26 28 30 32

### (6) 2열의 데이터들: 12 20 28 36

### (7) 왼쪽 대각선 데이터들: 10 20 30 40

### (8) 오른쪽 대각선 데이터들: 16 22 28 34 

``` python
mylist = [
    [10, 12, 14, 16],
    [18, 20, 22, 24],
    [26, 28, 30, 32],
    [34, 36, 38, 40]
]

#1
print(mylist[0][0])

#2
print(mylist[2][3])

#3
print(len(mylist))

#4
print(len(mylist[0]))

#5
for i in mylist[2]:
    print(i, end='', sep',')
print()

#6
for i in range(len(mylist)):
    print(mylist[i][1], end=' ')
print()

#7
for i in range(len(mylist)):
    for x in range(range(len(myist[i]))):
        if i == x:
            print(mylist[i][x], end='')
print()

#8
for i in range(len(mylist)):
    print(mylist[i][len(mylist)-1-i], end='')

```

### `3. 다음과 같은 내용으로 구성되는 이차원 리스트를 생성하고 행단위 합을 구하여 다음과 같이 출력하라.`

> **1행 10, 20, 30, 40, 50**
>
> **2행 5, 10, 15**
>
> **3행 11, 22, 33, 44**
>
> **4행 9, 8, 7, 6, 5, 4, 3, 2, 13**

아래와 같이 출력한다.

> **1행의 합은 x 입니다.**
>
> **2행의 합은 x 입니다.**
>
> **3행의 합은 x 입니다.**
>
> **4행의 합은 x 입니다.**

``` python
mylist = [
    [10, 20, 30, 40, 50],
    [5, 10, 15],
    [11, 22, 33, 44],
    [9, 8, 7, 6, 5, 4, 3, 2, 13]]

cnt = 0
for i in mylist:
    total = 0
    cnt += 1
    for hap in i:
        total += hap
    print(cnt, '행의 합은', total, '입니다.'')
```

### `4. 아래와 같은 내용으로 구성되는 2차원 리스트를 생성한다.`

> ​    **'B', 'C', 'A', 'A'**
>
>    **'C', 'C', 'B', 'B'**
>
>    **'D', 'A', 'A', 'D'**

### 다음 내용으로 구성되는 리스트를 하나 생성한다.

> 첫 번째 원소에는 'A' 문자의 개수 -> 4개
>
> 두 번째 원소에는 'B' 문자의 개수 -> x개
>
> .........
>
> 네 번째 원소에는 'D' 문자의 개수 -> ...개

### 다음과 같은 형식으로 출력한다.

> A는 x개 입니다.
>
> B는 x개 입니다.
>
> C는 x개 입니다.
>
> D는 x개 입니다.

``` python
mylist = [
    ['B', 'C', 'A', 'A'],
    ['C', 'C', 'B', 'B'],
    ['D', 'A', 'A', 'D']
]

newlist = []

for x in ['A', 'B', 'C', 'D']:
    cnt = 0
    for y in range(len(mylist)):
        cnt += mylist[y].count(x)
    newlist.append([x, mycount])
    
for char, cnt in newlist:
    print(char, '는', cnt, '개 입니다.')
```