# day 14: Inheritance

### `1. 상속하여 클래스 만들기`

> **person 클래스를 상속하여 Friend 라는 클래스를 아래와 같은 사양으로 구현한다.**
>
> **Friend 객체를 5개 생성한다.** 
>
> **생성된 객체들을 리스트에 저장한다.**
>
> **for문을 사용하여 리스트에 저장된 Friend 객체들을 꺼내서 다음 형식으로  출력한다.**

**이름               전화번호                메일주소**

**........................................................................**

**XXX              XXXXXXXXXX          XXX@XXXXXX (총 5개 행 작성)**



|               Person                |
| :---------------------------------: |
|              name: str              |
|          Person(name: str)          |
| getInfo(): str --> 이름을 리턴한다. |

|                            Friend                            |
| :----------------------------------------------------------: |
|                        phonenum : str                        |
|                          email: str                          |
| Friend(name:str, phonenum:str, email:str) -> 튜플로 리턴한다 |
|                        getInfo(): str                        |

``` python
# Class 상속 & 팩키 언팩킹 (튜플)

class Person:
    def __init__(self, name):
        self.name = name

    def getInfo(self):
        return self.name

class Friend(Person):
    def __init__(self, name, phonenum, email):
        super().__init__(name)
        self.phonenum = str(phonenum)
        self.email = str(email)

    def getInfo(self):
        return self.name, self.phonenum, self.email


f1 = Friend('Jane','0107777777','myemail@naver.com')
f2 = Friend('강아지', '01012345678', 'dog@gmail.com')
f3 = Friend('친구1', '01011112222', 'friend1@gmail.com')
f4 = Friend('친구2', '01033334444', 'friend2@gmail.com')
f5 = Friend('친구3', '01055556666', 'friend3@gmail.com')

print('이름  ', '전화번호   ', '     메일주소    ')
print('-'*40)

for f in [f1, f2, f3, f4, f5]:
    x,y,z = f.getInfo()
    print(x, y, z)


```

### `2. 클래스 변수와 인스턴스 변수를 포함한 클래스 만들기`

> **Card 라는 이름으로 클래스를 만들 때 위에서 모델링한 카드객체의 속성들은 Card 클래스의 멤버변수가 된다.**
>
> **(1) 객체의 속성값을 저장하는 멤버변수 4개를 정의한다. kind, number, width, height**
>
> **(2) Card 클래스의 객체를 생성한 후에 객체 정보를 print() 함수로 출력하거나 str() 함수로 문자열로 변환 시** 
>
>   **“카드의 종류: XX, 카드의 숫자 : XX, 카드의 크기 : (XX, XX)” 형식으로 정보가 리턴하도록 관련 특수 메서드를 오버라이딩한다.**

``` python
# 클래스 생성 & 오버라이딩(특수메소드 __str__ 사용)

class Card:
    width = 100
    height = 200

    def __init__(self, kind, number):
        self.kind = kind
        self.number = str(number)

    def __str__(self):
        return f"카드의 종류: {self.kind}, 카드의 숫자: {self.number}, 카드의 크기: ({Card.width},{Card.height})"


card1 = Card('Heart', '5')
card2 = Card('Spade', '9')
card3 = Card('Clover', '2')
card4 = Card('Diamond', '10')


for c in [card1, card2, card3, card4]:
    print(c)
```

