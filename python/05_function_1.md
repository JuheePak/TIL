# day 5: function

## 다양하게 함수 사용하기(Triangle, Gugu-dan)



### `1. 아래의 조건을 만족하는 함수를 만들고 결과를 출력하라.`

> **함수명: expr**
>
> **매개변수: 숫자 2개와 연산자 1개**
>
> **리턴값: 연산 결과 또는 None**
>
> 기능: 전달된 2개의 숫자에 대해 전달된 연산을 처리하고 그 결과를 리턴한다. 
>
> 연산자는 +, -, *, / 만 처리하며 그 외의 연산자는 연산을 하지 않고 None을 리턴한다.
>
> 숫자 2개와 연산자 1개를 전달하여 expr() 함수를 호출하고 리턴한 결과가 None 이면,
>
> **수행불가**를 출력하고 그렇지 않으면 **연산결과 : XX** 형식으로 출력한다.



```python
def expr(n1, n2, cal):
    if cal == '*':
        result = n1 * n2
    elif cal == '/':
        result = n1 / n2
    elif cal == '+':
        result = n1 + n2
    elif cal == '-':
        result = n1 - n2
    else:
        result = 'None'
    return result

n1 = int(input("n1: "))
n2 = int(input("n2: "))
cal = input('연산자: ')

result = expr(n1, n2, cal)

if result == None:
    print('수행불가')
else:
    print('연산결과: ', result)

```

### `2. 아래와 같은 조건을 만족하는 함수를 만들고 결과를 출력하라.`

> **함수명: print_triangle**
>
> **매개변수: 1개**
>
> **리턴값: 없음**
>
> 기능: 전달된 숫자 개수로 구성되는 삼각형을 출력한다. 출력 형식은 다음과 같다.
>
> **e.g. 2 전달시,**
>
> *****
>
> ******
>
> 단, **전달되는 아규먼트 값은 1 ~ 10 으로 제한한다.** 그 이외의 값이 전달된 경우 처리하지 않음



``` python
def print_triangle(n):
    if 0 < n < 11:
        for x in range(1, n+1): # or (0, num)
            for y in range(1, x+1): 
                print('*', end='') # 각 줄마다 별을 출력
            print('') # 줄바꿈 해주는 기능을 한다.
    else:
        return 

# print_triangle(3)

```



### `3. 아래와 같은 조건을 만족하는 함수를 만들고 결과를 출력하라`

> **함수명: print_triangle**
>
> **매개변수: 1개**
>
> **리턴값: 없음**
>
> 기능: 전달된 숫자 개수로 구성되는 **역삼각형**을 출력한다. 출력형식은 아래와 같다.
>
> **e.g.  2 전달시,**
>
> **@@**
>
> **@**
>
> 단, **전달되는 아규먼트 값은 1 ~ 10 으로 제한**한다. 그 이외의 값이 전달될 경우 처리하지 않음.



``` python
def print_triangle(n):
    if 0 < n < 11:
        for x in range(1, n+1):
            for y in range(n, x-1, -1): # 그 줄에 출력되는 특수문자의 개수.
                print('@', end='')
            print('')
    else:
        return
    
# print_triangle(4)    
```

### `4. 아래와 같은 조건을 만족하는 함수를 만들고 결과를 출력하라`

> **함수명: print_gugudan**
>
> **매개변수: 1개**
>
> **리턴값: 없음**
>
> 기능: 전달된 숫자의 구구단을 출력한다.
>
> - 전달된 아규먼트가 **int인지 체크**하고 아니면 그냥 리턴한다.
> - 전달된 아규먼트가 **1 ~ 9 사이인지 체크**하고 아니면 그냥 리턴한다.
> - 그 외의 경우 해당 단의 구구단을 **행 단위**로 출력한다.

```python
def print_gugudan(n):
    
    if type(n) != int:
        return
    elif n > 9 or n < 1:
        return 
    # 혹은 if type(n) is int and 1 <= n <= 9:
    else:
        for n in range(n, n+1):
            for hang in range(1, 10):
                print(n, '*', hang, '=', s*hang)
            print()
            
#print_gugudan(2)        

```



### `5. 아래와 같은 조건을 만족하는 함수를 만들고 결과를 출력하라`

> **함수명: differtwovalue**
>
> **매개변수: 2개**
>
> **리턴값: 연산 결과**
>
> 기능: 전달받은 2개의 데이터 중에서 큰 값에서 작은 값의 차를 리턴, 두 값이 동일하면 0을 리턴한다.
>
> **e.g. 10, 20이 전달되면 10을 리턴**
>
> **20, 5가 전달되면 15 리턴**
>
> **6과 6이 전달되면 0 리턴**
>
> 1부터 30 사이의 난수 2개를 추출하여 위에서 구현한 differtwovalue를 호출하고 결과를 아래와 같이 출력한다.
>
> **X와 Y의 차이는 W 입니다.**
>
> 를 5회 반복한다.

``` python
import random
def differtwovalue(n1, n2):
    if n1 == n2: # or n1 - n2 == 0, n1과 n2를 비교하는 식으로 통일하였음.
        return 0
    elif n1 > n2 :
        return n1 - n2
    elif n1 < n2 :
        return n2 - n1
    
for i in range(0, 5):
    x = random.randint(1, 30)
    y = random.randint(1, 30)
    result  = differtwovalue(x, y)
    
    print(x, '와', y, '의 차이는', result, '입니다.', sep='')
```

