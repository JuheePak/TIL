# day 13: class & instance

###` 1. Member 클래스의 인스턴스(객체)를 3개 생성하고 각각의 멤버 변수에 임의의 정보를 저장 후, 각 정보를 추출하여 다음 형식으로 출력하라.`

> ​    **회원1 : 이름(계정,암호,생년)**
>
> ​    **회원2 : 이름(계정,암호,생년)**
>
> ​    **회원3 : 이름(계정,암호,생년)**

![image-20200908154824886](C:\Users\juhee\TIL\python\image-20200908154824886.png)





``` python
class Member:

    def __init__(self):
        self.name = None
        self.account = None
        self.passwd = None
        self.birthyear = None
        
mem1=Member()
mem2=Member()
mem3=Member()
mem1.name='강아지'
mem2.name='고양이'
mem3.name='햄스터'
mem1.account = 1
mem2.account = 2
mem3.account = 3
mem1.passwd = '0000'
mem2.passwd = '0000'
mem3.passwd = '0000'
mem1.birthyear = 2002
mem2.birthyear = 2003
mem3.birthyear = 2004

print(f"회원1: {mem1.name}({mem1.account}, {mem1. passwd}, {mem1.birthyear})")
print(f"회원2: {mem2.name}({mem2.account}, {mem2. passwd}, {mem2.birthyear})")
print(f"회원3: {mem3.name}({mem3.account}, {mem3. passwd}, {mem3.birthyear})")
```



### `2. book 클래스의 인스턴스(객체) 5개를 생성하는데 인스턴스를 생성하면서 각각의 책 정보를 전달한다. 전달되는 책 정보는 임의로 정한다. 객체를 모두 생성한 후에 getBookInfo()를 호출하고 리턴 결과를 아래와 같이 출력하라.`

> **책이름**
>
> **저자**
>
> **가격**

![image-20200908155139355](C:\Users\juhee\TIL\python\image-20200908155139355.png)

``` python
class Book:
    def __init__(self, title = '파이썬 정복', author = '김형조', price = 22000):
        self.title = title
        self.author = author
        self.price = price

    def getBookInfo(self):
        return f"{self.title}, {self.author}, {self.price}"

book1 = Book()
book2 = Book('해리포터와 파이썬의 돌', 'J.K 롤링', 13000)
book3 = Book('해리포터와 파이썬의 기사단', 'J.K 롤링', 21000)
book4 = Book('해리포터와 파이썬의 죄수', 'J.K 롤링', 55000)
book5 = Book('해리포터와 파이썬의 잔', 'J.K 롤링', 43000)


for b in [book1, book2, book3, book4, book5]:
    print(b.getBookInfo().replace(',','\n'))
    print('-' * 10)

# OR

def printBookInfo(book):
    bookInfo = book.getBookInfo().split(',')
    for i in range(0, 3):
        print(bookInfo[i])
    print('-' * 10)

printBookInfo(book1)
```

