# day 11: Packing & Unpacking

### `1. 다음 리스트를 생성하고 각 문제의 답을 구하라.`

> listv3 = **[ 'p', 'y', 't', 'h', 'o', 'n' ]**

#### (1) v1, v2, v3, v4, v5, v6에 언패킹하여 저장한 후에 각 변수의 값을 행 단위로 화면에 출력한다.

#### (2) listv3 을 언패킹하여 print()함수에 전달하여 출력한다.

#### (3) listv3을 그냥 print() 함수에 전달하여 출력하고 2번과 3번의 차이를 설명하라.

``` python
listv3 = ['p', 'y', 't', 'h', 'o', 'n']

# (1) 언패킹하여 저장하고 행 단위로 화면에 출력
v1, v2, v3, v4, v5, v6 = listv3
print(v1, v2, v3, v4, v5, v6, sep = '\n')

# (2) listv3을 언패킹하여 print() 함수에 전달 출력
# print('p', 'y', 't', 'h', 'o', 'n')와 같은 결과
print(*listv3)

# (3) listv3을 그냥 print() 함수에 전달 출력
print(listv3) # 리스트 그대로 출력 ['p', 'y', 't', 'h', 'o', 'n']

# 2번의 출력값은 ''가 없는 형태로 출력되고, 3번은 리스트의 형태로 출력됨.
```



### `2.컴프리헨션 구문을 사용하여 다음에 제시된 데이터들로 구성되는 자료구조를 생성한다.`

#### (1) 난수 추출 함수를 사용하여 0~100 사이의 값 10개로 구성되는 리스트를 하나 생성한다.

#### (2) 위에서 생성된 리스트를 이용하여 다음과 같이 구성되는 딕셔너리를 생성한다. 추출된 숫자가 60점 이상이면 pass 로 처리한다.

>  **{1: 'nopass', 2:'nonpass',........., 10: 'pass'}**

``` python
import random

mylist = [random.randint(1, 100) for s in range(10)]
# print(mylist)

passnpass = {x+1:'pass' if mylist[x] >= 60 else 'nonpass' for x in range(len(mylist))}
print(passnpass)

# 만약 컴프리헨션이 아닌 코드를 짠다면- pass/nopass의 결과만 출력함.
for x, y in enumerate(mylist, 0):
   if mylist[x] >= 60:
       print('pass')
   else:
       print('nopass')
```

#### 컴프리헨션은 일반적인 코드를 작성하였을 때와 비교했을 때 속도가 빠르며, 코드도 간단하게 작성할 수 있다. 여러번 반복하여 내 것으로 만들자

#### 또 packing/unpacking도 파이썬에 있는 강력한 기능 중 하나이다. 잘 연습하자. 매번 헷갈린다

