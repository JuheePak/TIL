# day 4: for

## 반복문

### `1. 다음과 같은 결과가 출력되도록 구현하라.`

> **1 2 3 4 5 6 7 8 9 10**

``` python
for i in range(1, 11):
print(i, end=' ', sep=' ')
```

### `2. 다음과 같은 결과가 출력되도록 구현하라.`

> **9 : 홀수**
>
> **8 : 짝수**
>
> **7 : 홀수**
>
> **6 : 짝수**
>
> **5 : 홀수**
>
> **4 : 짝수**

``` python
for i in range(9, 3, -1):
    if i % 2 == 0:
        print(i, ": 짝수", sep='')
    else:
        print(i, ": 홀수", sep='')
```



### `3. 1부터 10 사이의 난수를 하나 추출한다. 30부터 40 사이의 난수를 하나 추출한다. 첫번째 난수부터 두번째 난수까지의 숫자들 중 짝수의 합을 구해 아래 형식으로 출력하라.`

> **X 부터 Y 까지의 짝수의 합 : XX**

``` python
import random

ranNum1 = random.randint(1, 10)
ranNum2 = random.randint(30, 40)

sum = 0
for num in range(ranNum1, ranNum2 +1):
    if num % 2 == 0:
        sum = sum+num
print(ranNum1, '부터', ranNum2, '까지의 짝수의 합', sum)        
```



### `4. evenNum 변수와 oddNum 변수의 값을 0으로 대입한다.`

### `1부터 100까지의 값 중에서 짝수의 합은 evenNum에 누적하고, 홀수의 값은 oddNum에 누적한다. 수행결과는 아래와 같이 출력한다.`

> **1부터 100까지의 숫자들 중에서**
>
> **짝수의 합은 XXX 이고**
>
> **홀수의 합은 YYY 이다.**

``` python
evenNum = 0
oddNum = 0

for sumNum in range(1, 100):
    if sumNum % 2 == 1:
        oddNum = oddNum + sumNum
    else:
        evenNum = evenNum + sumNum
        
print('1부터 100까지의 숫자들 중에서')
print('짝수의 합은', evenNum, '이고', sep='')
print('홀수의 합은', oddNum, '이다.', sep='')
```



### `5. 1부터 50까지의 숫자 중에서 3의 배수에 해당하는 값의 합을 구한다. 단, 5의 배수는 제외한다.`

### *continue 사용하지 않고 해결*

> **결과 = 318**

``` python
sunNum = 0

for num in range(1, 50):
    if num % 3 == 0 and num % 5 != 0:
        sunNum = sumNum + num
        
print('결과 = ', sunNum, sep='')
```



### `6. continue를 사용하여 5과 같은 결과를 출력한다.`

``` python
sumNum = 0

for num in range(1, 50):
    if num % 5 == 0:
        continue
    if num % 3 == 0:
        sumNum += num
        
print('결과 = ', sumNum, sep='')
```

