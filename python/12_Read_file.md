# day 12: read file & Try-except-else-finally

### `1. 다음 내용을 생성하여 c:/iotest/today.txt 라는 파일을 저장한다. c:/iotest 디렉토리의 존재여부를 체크하고 존재하지 않으면 생성한다. 출력 내용은 아래와 같다.`

> **오늘은 2020년 xx월 xx일입니다. (현재 날짜)**
>
> **오늘은 x요일입니다.**
>
> **xxx는 x요일에 태어났습니다.**

### `위의 내용을 저장한 후 화면에는 저장이 완료되었습니다. 를 출력한다.`

``` python
import os
import datetime
import calendar

directory_name = 'C:/iotest'
exist_directory = os.path.isdir(directory_name)
if not exist_directory:
    os.mkdir("c:/iotest")

f = open("c:/iotest/today.txt", "wt", encoding="UTF-8")

now = datetime.datetime.now()
day = calendar.weekday(2020, 9, 7)
bday = calendar.weekday(1993, 6, 15)

txt = f"""오늘은 {now.year} 년 {now.month:>02}월 {now.day:>02}일입니다.
xx는 {bday}요일에 태어났습니다."""

f.write(txt)
f.close()
```



### `2. 제공된 sample.txt 파일을 읽고 sample_yyyy_mm_dd.txt 파일에 그대로 출력하는 프로그램을 구현한다. 이 파일은 append 모드로 오픈하여 여러 번 테스트하면 sample.txt 파일의 내용이 sample_yyyy_mm_dd.txt 파일에 계속 추가되게 한다. `

### `위의 내용을 파일에 저장하는 기능이 정상적으로 수행되면 화면에 저장이 완료되었습니다. 를, FileNotFoundError 발생시 오류에 대한 메시지 정보를 출력하고 종료한다.`

``` python
import datetime

fdr = None
fdw = None # 숫자를 넣을 상황인데 정해지지 않았으면 보통 0 을 쓰고, 아니라면 None을 많이 씀

# 파일명 만들기
now = datetime.datetime.now()
writeFileName = 'sample_' + now.isoformat()[0:10] + '.txt'

# print(writeFileName) return sample_2020-09_07.txt

try:
    # 파일 처리
    fdr = open("../sample.txt", "rt", encoding="UTF-8")
    fdw = open(writeFileName, "at", encoding="UTF-8")

    for line in fdr: # in 뒤에 open으로 사용된 객체도 쓸 수 있다. open의 행단위로 읽음
        fdw.write(line)
    fdw.write('\n\n') # 개행처리 두번씩

except FileNotFoundError as e:
    print(e)

else:
    print("저장이 완료되었습니다.")

finally:
    if fdr:
        fdr.close()

    if fdw:
        fdw.close()
```



### `3. 프로그램 수행 중간에 년도와 월을 입력받아 해당년과 월의 달력을 출력한다. 년도와 월은 숫자로 입력받아야 하며 숫자가 입력되지 않아서 발생하는 에러를 대비해야한다.`

### `ValueError 처리를 통해 숫자가 입력되지 않은 경우 메시지를 내보내고, 다시 입력받는다. 년도와 월이 제대로 입력될 때까지 반복한다.`

``` python
import calendar

while True:
    year = input('연도를 숫자로만 입력해주세요: ')
    month = input('월을 숫자로만 입력해주세요: ')

    try:
        my_year = int(year)
        my_month = int(month)

        print(calendar.month(my_year, my_month))
        break

    except ValueError as v:
        print(v)

print('달력이 출력되었습니다.')
```



### `4. 제공된 yesterday.txt 파일을 읽고 이 문서에 "Yesterday" 가 몇 개 들어있는지 개수를 세어 출력한다. (대소문자는 구분하지 않는다.)`

### ` FileNotFoundError 발생 시 파일을 읽을 수 없어요 를 출력하고 종료한다. 에러가 발생하지 않으면 Number of a Word 'Yesterday' X 를 출력하고 종료한다.` 

### ` 에러 발생 여부와 관계 없이 수행완료!! 를 출력하고 종료한다. (Try-except-else-finally를 모두 사용하여 해결한다.)`

``` python
f = open("yesterday.txt", "rt", encoding="UTF-8")

try:
    yday = f.read().lower().count('yesterday')

except FileNotFoundError:
    print('파일을 읽을 수 없어요')
else:
    print(F"Number of a Word 'Yesterday' {yday}")
finally:
    print('수행완료!!')
```

