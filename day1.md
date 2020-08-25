# day1: Introduction of Python

 ## 기본적인 연산

### `1.time 이라는 변수에 32140을 대입한다. 이 값은 초단위의 값이다. time이라는 변수의 값으로 연산하여 `

### **8시간 55분 40초** `형식으로 변환하여 출력한다.`

```python
time = 32140
a = int(time//(60*60))
print(a, "시간", ((time-(a*60*60))//60), " 분 ", int(time%60), "초")
```

단, 시간의 숫자와 한글 사이에 공백이 존재해서는 안 된다.(문제에 출력 결과 확인)

그걸 방지하고자 변수를 시, 분, 초마다 변수를 지정해주고 출력하는 방법도 있다.

```python
time = 32140
hour = int(time//(60*60))
min = int(time-(a*60*60))//60
sec = int(time%60)

print(hour, '시간', min, '분', sec, '초')
```



### `2. 아래와 같은 결과값을 출력하라.`

![image-20200825003933966](C:\Users\juhee\AppData\Roaming\Typora\typora-user-images\image-20200825003933966.png)

IDLE을 사용한 결과값이다. 무시하자 :)

```python
a = input("문자 한개를 입력하세요: ")
print(a, '문자의 코드 값은', hex(ord('A')), '입니다.')

b = input("문자 한개를 입력하세요: ")
print(b, '문자의 코드 값은', hex(ord('B')), '입니다.')

c = input("문자 한개를 입력하세요: ")
print(c, '문자의 코드 값은', hex(ord('a')), '입니다.')

d = input("문자 한개를 입력하세요: ")
print(d, '문자의 코드 값은', hex(ord('가')), '입니다.')

e = input("문자 한개를 입력하세요: ")
print(e, '문자의 코드 값은', oct(ord('e')), '입니다.')

```



### `3.다음 기능을 구현하라. `

![image-20200825004121748](C:\Users\juhee\AppData\Roaming\Typora\typora-user-images\image-20200825004121748.png)

```python
a = int(input("숫자 1입력: "))
b = int(input("숫자 2입력: "))
print(a+b)
print(a*b)
print(a**b)
```



### `4.num 변수와 su 변수를 가지고 +, -, *, / 연산을 수행한 결과를 출력한다. 각 연산을 수행할 때마다 연산 결과를 num 변수에 대입한 후 다음 형식으로 출력한다. `

### `num = 20, su = 5`

![image-20200825004336986](C:\Users\juhee\AppData\Roaming\Typora\typora-user-images\image-20200825004336986.png)

```python
num+=su
print(num)
print('-*-'*10)
num*=su
print(num)
print('-*-'*10)
num-=su
print(num)
print('-*-'*10)
num=num/su
print(num)
print('-*-'*10)
```

