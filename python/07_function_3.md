# day 7: function

## 응용문제 - 함수, 가변아규먼트

### `1. 다음 조건을 만족하는 함수를 만들고 값을 출력하라`

> **함수명: print_triangle_withdeco**
>
> **매개변수: 숫자와 데코문자 총 2개. 데코문자는 기본값을 %로 갖는다.**
>
> **리턴값: 없음**
>
> 기능: 전달된 숫자 개수로 구성되는 삼각형을 출력한다.
>
> e.g. 숫자 2 전달시,
>
>    %
>
> %%
>
> 숫자 5와 데코문자 '2' 전달시,
>
>   *
>
> **
>
> 전달되는 **아규먼트 값은 1~10으로 제한**한다. 그 이외의 값이 전달될 경우 처리하지 않는다.

``` python
def print_triangle_withdeco(num, deco = '%'):
    if 0 < num < 11:
        for x in range(1, num+1):
            for y in range(num-x): # 공백
            	print(' ', end='')
            for z in range(1, x+1):
                print(deco, end='')
            print('')
    else:
        return
    
print_triangle_withdeco(4, '$')
print_triangle_withdeco(7, '@')    
```



### `2. 다음 값으로 구성되는 리스트를 생성하여 listnum에 저장하고, 최댓값을 추출하여 아래와 같이 출력한다.`

> 10, 5, 7, 21,4, 8, 18
>
> **최댓값 : 21**

``` python
listnum = [10, 5, 7, 21, 4, 8, 18]

print('최댓값:', max(listnum))
```



### `3. 2번 문제와 같은 list를 생성하고 최솟값을 출력하라.`

``` python
listnum = [10, 5, 7, 21, 4, 8, 18]

print('최솟값:', min(listnum))
```



### `4. 3번과 같은 list를 생성하고 listnum에 저장하라. 저장된 값들 중에서 최대값과 최소값을 추출하여 아래와 같이 출력한다.`

> **최솟값: 5, 최댓값: 21**

``` python
listnum = [10, 5, 7, 21, 4, 8, 18]

big_value = listnum[0]
min_value = listnum[0]

for cnt in range(1, len(listnum)):
    if big_value < listnum[cnt]:
        big_value = listnum[cnt]
        
for cnt in range(1, len(listnum)):
    if min_value > listnum[cnt]:
        min_value = listnum[cnt]

print('최대값:', big_value, '최솟값:', min_value, end=' ')        

# Or min과 max를 써서 구하면 쉽다.
# print('최솟값:',min(listnum), '최댓값:',max(listnum))
```



### `5. 비어있는 리스트 하나 생성하여 listnum 변수에 저장한다. 1~50 사이의 난수를 10개 추출하여 listnum에 추출 순서대로 저장(for문 사용)한다. `

#### (1) listnum의 모든 값을 출력한다.

#### (2) 인덱싱 방법으로 listnum의 첫번째 데이터를 출력한다.

#### (3) 인덱싱 방법으로 listnum의 마지막 데이터를 출력한다.

#### (4) 슬라이싱 방법으로 listnum의 데이터를 역순으로 모두 출력한다.

``` python
import random
listnum = []
ranNum = random.randint(1, 50)
for i in range(10):
    ranNum = random.randint(1, 50)
    while ranNum in listnum:
        listnum.append(ranNum)
#(1)
print(listnum)

#(2)
print(listnum[0])

#(3)
print(listnum[len(listnum)-1])

#(4)
print(listnum[::-1])


```



### `6. 다음 조건을 만족하는 함수를 구현하고 값을 출력하라.`

> **함수명: sumEven1**
>
> **매개변수: 가변형, 전달받을 수 있는 아규먼트의 개수에 제한이 없다.**
>
> **리턴값: 1개**
>
> 기능: 아규먼트는 **1 이상의 숫자**만 온다. **짝수에 해당하는 숫자의 합만 계산하여 리턴한다.** 전달된 아규먼트중 짝수가 없다면 **0을 리턴**한다. 아규먼트가 전달되지 않으면 **-1을 리턴**한다.

``` python
def sumEven1(*num):
    if len(num) == 0:
        return -1
    
    sum = 0
    for n in num:
        if n%2 == 0:
            sum +=n
    return sum

#print(sumEven1(1, 2, 4, 19, 8))
```



### `7. 다음 조건을 만족하는 함수를 구현하고 값을 출력하라. 

> **함수명: sumAll**
>
> **매개변수: 가변형, 전달받을 수 있는 아규먼트 개수에 제한이 없다.**
>
> **리턴값: 1개**
>
> 기능: 아규먼트 데이터 타입에는 제한이 없다. 전달된 아규먼트의 타입을 체크하여 **숫자만 처리하고 숫자가 아닌 데이터는 무시한다.** 아규먼트가 전달되지 않았거나 전달되었다 하더라도 숫자가 없으면 **None을 리턴**한다.



``` python
def sumAll(*arg):
    sum = 0
    value_flag = 0
    if len(arg) == 0:
        return None
    else:
        for data in arg:
            if type(arg) == int:
                value_flag = 1
                sum += int(data)
        if value_flag == 0:
            return None
        else:
            return sum
        
print(sumAll('가', '22', 4, 9))            
```



