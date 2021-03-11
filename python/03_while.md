# day 3: while

## 반복문

### `1. 5부터 10 사이의 난수룰 추출한다. 1부터 추출된 숫자의 값까지 각 숫자들의 제곱값을 행단위로 출력한다.`

> 4가 추출될 경우,
>
> 1 -> 1
>
> 2 -> 4
>
> 3 -> 9
>
> 4 -> 16 

``` python
import random
i = random.randint(5, 10)

num = 1
while num <= i:
    print(num, '->', num**2)
    num += 1
```

### `2. while 반복문을 사용하여 다음 기능을 구현하라.`

> 1부터 6사이의 2개의 난수룰 추출하여 각각 **pairNum1, pairNum2**로 저장한다.
>
> 추출된 2개의 숫자가 다르면 값의 크기를 비교하여 **"~가 ~보다 작다/크다"**를 출력한다.
>
> 추출된 2개의 숫자가 동일하면 **"게임 끝"** 이라는 메시지를 출력하고 종료한다.

```python
import random

while True:

    pairNum1 = random.randint(1, 6) 
    pairNum2 = random.randint(1, 6)

    print('num1: ', pairNum1, 'num2: ', pairNum2)

    if pairNum1 > pairNum2:
        print('pairNum1이 pairNum2 보다 크다')
    elif pairNum1 < pairNum2:
        print('pairNum1이 pairNum2 보다 작다')
    else:
        print('게임 끝')
        break
```

2개의 난수를 break 될 때까지 무한으로 추출하기 때문에 while 문 안쪽에 써줘야한다.



### `3. while 문으로 무한루프 생성하기`

### `(1) 0부터 30까지의 난수룰 추출한다. 추출된 숫자가 1이면 'A', 2면 'B'.. 26이면 'Z'를  출력하는데, 0이 추출되거나 27~30이 출력되면 반복을 끝낸다.`

> 출력되는 형식:
>
> **B(2)**
>
> **A(1)**
>
> **D(4)**
>
> **수행횟수는 X 번 입니다.**

``` python
import random
count = 0

while True:
    ranNum = random.randint(1, 30)
    count += 1
    if ranNum == 0 or (26 < ranNum <= 30):
        print("수행횟수는", count-1, "번 입니다.")
    else:
        print(chr(ranNum+64), '(',ranNum,')', sep='')
```

### `4. while 문으로 반복처리한다.`

### `(1) 사용자로부터 월에 해당되는 숫자를 하나 입력받는다.`

> 입력받은 값이 1~12 사이인 경우, 
>
> 12, 1, 2 이면 **X월은 겨울**
>
> 3, 4, 5 이면 **X월은 봄**
>
> 6, 7, 8 이면 **X월은 여름**
>
> 9, 10, 11 이면 **X월은 가을**
>
> 을 출력한다. 입력받은 숫자가 1~12 사이의 숫자가 아니면,
>
> **1~12 사이의 숫자를 입력해주세요! **를 출력하고 종료한다.

``` python
while True:
    
    s = int(input("1부터 12까지 범위에서 숫자 하나를 입력해주세요."))
    
        if 0 < s < 13:
        if s == 12 or s == 1 or s == 2: 
            print(s,"월은 겨울", sep='')
        elif 2 < s < 6:
            print(s,'월은 봄', sep='')
        elif 6 < s < 9:
            print(s,'월은 여름', sep='')
        else:
            print(s,'월은 가을', sep='')
    else:
        print('1과 12사이의 숫자를 입력해주세요!')
        break
```

