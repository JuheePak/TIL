# day 10:  comprehension

### `1. 아래 조건을 만족하는 함수를 만들고 값을 출력하라.`

> **함수명: createList**
>
> **매개변수: 가변 아규먼트를 받는 매개변수 1개**
>
> **매개변수 명은 type이며 기본값은 1이다.**
>
> **리턴값: 1개**
>
> 기능: 가변 아규먼트로 전달되는 값들을 가지고 정해진 규격의 리스트를 생성하여 리턴한다. 가변아규먼트가 전달되지 않은 경우에는 1~30까지의 값을 가지고 정해진 규격의 리스트를 생성하여 리턴한다.
>
> **type이 2이면** 주어진 데이터 값들에서 짝수에 해당되는 데이터들만 가지고 리스트 생성
>
> **type이 3이면** 주어진 데이터 값들에서 홀수에 해당되는 데이터들만 가지고 리스트 생성
>
> **type이 4이면** 주어진 데이터 값들에서 10보다 큰 데이터들만 가지고 리스트 생성
>
> **type이 1이면** 주어진 데이터 값 모두를 가지고 리스트를 생성
>
> 리스트 생성은 리스트 컴프리헨션(지능형 리스트) 구문을 사용한다.

``` python
def createList(*args, type):
    type = 1
    if len(args) == 0:
    if type == 1:
        return list(args)
    if type == 2:
        return [n for n in args if n%2 == 0 ]
    if type == 3:
        return [n for n in args if n%2 != 0 ]
    if type == 4:
        return [n for n in args if n > 10]
```



### `2. 다음 조건을 만족하는 함수를 구현하고 값을 출력하라.`

> **함수명: mydict**
>
> **매개변수: 가변 키워드형(키=값 형식으로 전달받을 수 있는 아규먼트 개수에 제한이 없다.)**
>
> **리턴값: 1개**
>
> **기능: 딕셔너리 컴프리핸션(지능형 딕셔너리) 구문을 사용.**

``` python
def mydict(**args):
    return {'my_'+k:v for k, v in args.items()}
    # return new_list

print('#여러가지 값 출력: ')
print(mydict(a=1))
print(mydict(a= 2, b = 1))
print(mydict(name = '파이썬', year = '1960'))
print('#빈 new_list 출력: ')
print(mydict()) # args.items()에 전달되지 않기 때문에 for문이 수행되지 않음.
# 비어있는 딕셔너리가 생성됨.    
```



### `3. 아래 조건을 만족하는 함수를 구현하라.`

> **함수명: myemail_info**
>
> **매개변수: 이메일 주소 문자열 1개**
>
> **리턴값: 2개의 원소를 갖는 튜플**
>
> 기능: 전달된 이메일 주소 문자열에서 **@를 기준으로 쪼개서 튜플**을 만들어 리턴한다. 단, 전달된 **문자열에 @가 없으면 None을 리턴**한다.

``` python
def myemail_info(email):
    if '@' not in email:
        return None
    else:
        splitEmail = email.split('@')
        return tuple(splitEmail)
    
print(myemail_info('xxxxxxx@naver.com'))
print(myemail_info('yyyyyyy@gmail.com'))
print(myemail_info('lol'))   
```



### `4. 아래 문제의 해당되는 코드를 구현하라.`

#### (1) s1 = 'pythonjavascript' 의 길이를 출력하라.

#### (2) s2 = '010-4444-5555' 에서 01044445555를 출력하라.

#### (3) s3 = 'PYTHON' 에서 NOHTYP를 출력한다.

#### (4) s4 = 'Python' 에서 python을 출력한다.

#### (5) s5 = 'https://www.python.**org/**'에서 www.python.org 만을 뽑아 출력한다.

#### (6) 다음 주민등록 번호에서 7자리의 숫자를 사용해서 여자, 남자를 판별하라. (2, 4: 여자, 1, 3: 남자)

> s6 = '891022-2435849'

#### (7) s7 = '100'에서 s7 값을 정수형 숫자로 그리고 실수형 숫자로 변환하여 출력하라.

#### (8) s8 = 'The Zen of Python' 에서 'n'의 문자가 몇개인지 출력하라.

#### (9) s8에서 "Z"의 위치를 출력하라.

#### (10) s8에서 모두 대문자로 변환한 후 공백단위로 분리해서 리스트로 만들어 출력한다.

``` python
s1 = 'pythonjavascript'
s2 = '010-7777-9999'
s3 = 'PYTHON'
s4 = 'Python'
s5 = 'https://www.python.org/'
s6 = '930615-3150314'
s7 = '100'
s8 = 'The Zen of Python'

# 길이 출력
print(len(s1))

#- 삭제하고 출력
split_s2 = s2.split('-')
for c in split_s2:
    print(c, end='')

# 파이썬 거꾸로 출력
print()
print(s3[::-1])

# 대문자 소문자로 변환
print(s4.lower())

# http:// 제거
print(s5[8:-1])

# 주민번호에서 여자 남자 판별하게, 주민번호 ' ' 문자형!
if s6[7] == '2' or s6[7] == '4':
    print('여자입니다.')
else:
    print('남자입니다.')

# 정수, 실수형으로 변환
s7_1 = int(s7[0:4])
print('정수형 %d' % s7_1)
print('실수형 %f' % s7_1)

# n의 갯수 출력
print(s8.count('n'))

# Z의 위치 출력
print(s8.find('Z')) # Or index method 사용도 가능

# 대문자변환, 공백으로 분리, 리스트로 만들어 출력
lower_s8 = s8.lower()
print(lower_s8)
split_lower_s8 = lower_s8.split(' ')
print(split_lower_s8)

print(f'{s8.upper().split()}')

#혹은 한줄로 아래처럼 가능
print(f'{s8.upper().split(" ")}')
```



### `5. 아래 리스트 항목 중에서 소문자만 추출하여 리스트를 생성하고 listv2에 저장/출력하라. (리스트 컴프리헨션을 사용할 것!)`

> **listv1 = ["A", "b", "c", "D", "e", "F", "G", "h"]**

``` python
listv1 = ['A', 'b', 'c', 'D', 'e', 'F', 'G', 'h']

listv2 = [i for i in listv1 if i.islower() ]
print(listv2)
```

