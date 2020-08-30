# day 6: function

## 응용문제

- 지금까지 배운 if, while, for, 기본연산(*, +, -, /), input 등 종합하여 연습하는 문제
- 제공된 OperTestApp1.py를 사용한다.
- Cheer up :)



### `1. 제공받은 OperTestApp1.py를 복사하여 OperTestApp2.py를 생성하고 OperTestApp1의 기능을 3번 반복하게 소스를 변경하라.`

> 제공받은 OperTestApp1.py

``` python
print("*입력한 숫자만큼 데코문자를 출력하는 프로그램입니다.*")


deco = input("데코문자를 입력하세요 : ")
number = int(input("출력횟수를 입력하세요 : "))
for i in range(number) :
    print(deco, end="")
print()
print("*수행 종료됩니다.*")
```

> 내가 작성한 OperTestApp2.py

``` python
print("*입력한 숫자만큼 데코문자를 출력하는 프로그램입니다.*")

for x in range(3):
    deco = input("데코문자를 입력하세요 : ")
    number = int(input("출력횟수를 입력하세요 : "))
    for i in range(number) :
        print(deco, end="")
    print()
    
print("*수행 종료됩니다.*")   
```



### `2. OperTestApp1.py를 복사하여 OperTestApp3.py를 생성하고 OperTestApp1의 기능을 원할 때까지 반복하는 소스를 작성한다. 숫자와 데코 문자를 받아서 수행하고, "계속 수행할까요?(y/n)"라는 메시지와 함께 입력을 받아 n이 입력되면 종료한다.`

```python
print("*입력한 숫자만큼 데코문자를 출력하는 프로그램입니다.*")

while True:
    deco = input("데코문자를 입력하세요 : ")
    number = int(input("출력횟수를 입력하세요 : "))
    for i in range(number) :
        print(deco, end="")
    print()
    
    q = input("계속 수행할까요? (y/n)")
    
    if q == 'n':
        break
        
print("*수행 종료됩니다.*")        
```



### `3. OperTestApp3.py를 복사하여 OperTestApp4.py를 생성하고 입력받은 숫자가 1보다 작으면 "출력회수는 0보다 큰 숫자를 입력하세요!" 메시지를 출력한 후에 다시 입력받는 것부터 시작한다.`

``` python
print("*입력한 숫자만큼 데코문자를 출력하는 프로그램입니다.*")

while True:
    deco = input("데코문자를 입력하세요 : ")
    number = int(input("출력횟수를 입력하세요 : "))
    
    if number < 1:
        print('출력회수는 0보다 큰 숫자를 입력하세요!')
        continue # continue를 여기에 달아야 위에 number 입력받는 부분으로 돌아가 반복
        
    else:
        for i in range(number) :
        print(deco, end="")
    print()
    
    q = input("계속 수행할까요? (y/n)")
    
    if q == 'n':
        break
        
print("*수행 종료됩니다.*")        
```

