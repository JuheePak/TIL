# day 2: if

## 조건문

### `1. 다음에 제시된 기능을 구현하고 소스파일을 제출하라.`

### `(1) num 이라는 변수에 사용자로부터 숫자 하나를 입력받는다. `

### `(2) 입력받은 숫자가 10보다 큰 경우에만 OK라는 문자열을 출력한다.`

```python
num = int(input('숫자를 하나 입력해주세요: '))

if num > 10:
    print("OK")
```



### `2. `

### `(1) colorName 이라는 변수에 사용자로부터 컬러 이름을 하나 입력받는다.`

### `(2) 입력받은 컬러명이 red이면 #ff0000을 출력한다. 입력받은 컬러명이 red가 아니라면 #000000을 출력한다.`

```python
colorName = str(input('컬러 이름을 하나 입력해주세요: '))

if colorName == 'red':
    print('#ff0000')
else:
    print('#000000')

    # #000000은 검정색
```



### `3.`

### `(1) grade 라는 변수에 1부터 6사이의 숫자를 랜덤추출하고 저장한다. 조건 평가 시 and 연산자를 사용한다.`

### `(2) grade의 값이 1 또는 2 또는 3이라면 다음 결과를 출력한다.`

> **x 학년은 저학년입니다.**

### `grade의 값이 4 또는 5 또는 6이라면 다음 결과를 출력한다.`

> **x 학년은 고학년입니다.**

```python
import random
grade = random.randint(1, 6)

if grade != 4 and 5 and 6:
    print(grade,'학년은 저학년입니다.', sep='')
else:
    print(grade, '학년은 고학년입니다.', sep='')    
```

### `4.`

### `(1) grade 라는 변수에 1부터 6 사이의 숫자를 랜덤추출하여 저장한다. 조건 평가시 or 연산자를 사용한다.`

### `(2) grade의 값이 1 또는 2또는 3이면 다음 결과를 출력한다.`

> **x 학년은 저학년입니다.**

### `(3) grade 의 값이 4 또는 5 또는 6이면 다음 결과를 출력한다.`

> **x 학년은 고학년입니다.**

```python
import random
grade = random.randint(1, 6)

if grade == 1 or grade == 2 or grade == 3:
    print(grade,"학년은","저학년입니다.", sep=' ')
else:
    print(grade,"학년은","고학년입니다.", sep=' ')
```

### `5.`

### `(1) score 라는 변수에 0부터 100 사이의 숫자를 추출하고 저장한다. `

### `(2) score 라는 변수의 값의 크기에 따라서 다음의 내용을 출력한다. print 함수를 5개 사용하여 해결한다.`

> **score 변수의 값이 90~100 이면  xx점은 A등급입니다.**

> **score** **변수의 값이 80~89 이면  xx점은 B등급입니다.**

> **score** **변수의 값이 70~79 이면  xx점은 C등급입니다.**

> **score** **변수의 값이 60~69 이면  xx점은 D등급입니다.**

> **score 변수의 값이 0~59 이면  xx점은 F등급입니다**.

```python
import random
score = random.randint(0, 100)

if 90 <= score <= 100:
    print(score,'점은 A등급입니다.')
elif 80 <= score <= 89:
    print(score,'점은 B등급입니다.')
elif 70 <= score <= 79:
    print(score,'점은 C등급입니다.')
elif 60 <= score <= 69:
    print(score,'점은 D등급입니다.')
else:
    print(score,'점은 F등급입니다.')

```



### `6. 5번의 문제를 하나의 print 함수를 사용하여 결과를 출력한다.`

```python
import random
score = random.randint(0, 100)
grade = str()

if 90 <= score <= 100:
    grade = 'A'
elif 80 <= score <= 89:
    grade = 'B'
elif 70 <= score <= 79:
    grade = 'C'
elif 60 <= score <= 69:
    grade = 'D'
else:
    grade = 'F'

print(score,'점은 ',grade,'등급입니다.')
```

### `7.`

### `(1) num 이라는 변수에 사용자로부터 숫자 하나를 입력받는다.`

> 입력받을 때의 메시지 -> **1부터 10 사이의 숫자를 하나 입력하세요.**

### `(2) 입력 받은 숫자가 1부터 10사이의 숫자가 아니면 아래와 같은 메시지를 출력합니다.`

> 1부터 10 사이의 숫자를 하나 입력하세요: 0
>
> **1부터 10 사이의 값이 아닙니다.**

### `(3) 입력 받은 숫자가 1부터 10사이의 숫자이면 다음과 같이 처리합니다.`

> 1부터 10 사이의 숫자를 하나 입력하세요: 2
>
> 2 : 홀수
>
> 1부터 10 사이의 숫자를 하나 입력하세요: 4
>
> 4: 짝수

``` python
num = int(input("1부터 10사이의 숫자를 하나 입력하시오: "))

if 0 < num < 10:
    if num % 2 == 0:
        print(num, ": 짝수", sep=' ')
    else:
        print(num, "홀수", sep='')
else:
    print("1부터 10사이의 값이 아닙니다.")
```

### `8.`

### `(1) operNum 이라는 변수에 1부터 5사이의 랜덤값을 추출하여 대입한다.`

### `(2) 추출된 값이 1이면 300 과 50 의 덧셈 연산을 처리한다.`

 ### `추출된 값이 2이면 300 과 50 의 뺄셈 연산을 처리한다.`

### ` 추출된 값이 3이면 300 과 50 의 곱센 연산을 처리한다.`

### ` 추출된 값이 4이면 300 과 50 의 나눗셈 연산을 처리한다.`

### ` 추출된 값이 5이면 300 과 50 의 나머지 연산을 처리한다.`

### `(3) 출력 형식 (단, 결과를 출력하는 수행 문장은 한 번만 구현한다.)`

> **결과값 : XX**

``` python
import random
operNum = random.randint(1, 5)
a = 300
b = 50
result = int()

if operNum == 1:
    result = a+b
elif openNum == 2:
    result = a-b
elif openNum == 3:
    result = a*b
elif openNum == 4:
    result = a/b
else:
    result = a%b
print('결과값 :', result)
    
```

