## day 19: dplyr package

### `1. ggplot2 패키지에서 제공되는 mpg 라는 데이터 셋의 구조를 확인한다. 이 mpg 를 데이터프레임으로 변환하여 mpg 에 저장한다.(as.data.frame())`

이 mpg 를 데이터프레임으로 변환하여 mpg 에 저장한다.(as.data.frame())

install.packages("ggplot2")

str(ggplot2::mpg)

mpg <- as.data.frame(ggplot2::mpg)

``` R
library(dplyr)
library(ggplot2)

str(mpg)
mpg <- as.data.frame(mpg)
```



### `1-1 mpg의 구조를 확인한다.`

``` R
# 1-1
str(mpg)
```



### `1-2 mpg 의 행의 개수와 열의 개수를 출력한다.`

```R
# 1-2
dim(mpg)
```



### `1-3 mpg의 데이터를 앞에서 10개 출력한다.`

```R
#1-3
head(mpg, 10)
```



### `1-4 mpg의 데이터를 뒤에서 10개 출력한다.`

```R
#1-4
tail(mpg, 10)
```



### `1-5. mpg의 데이터를 GUI 환경으로 출력한다.`

```R
#1-5
View(mpg)
```



### `1-6 mpg를 열 단위로 요약한다.`

```R
#1-6
summary(mpg)
```



### `1-7 mpg 데이터셋에서 제조사별 차량의 수를 출력한다.`

```R
#1-7
mpg %>% count(manufacturer)
```



### `1-8 mpg 데이터셋에서 제조사별 그리고 모델별 차량의 수를 출력한다.`

```R
#1-8
mpg %>% count(manufacturer, model)
```



### `2. 다음에 제시된 문제를 각각 2-1, 2-2 으로 넘버링 하여 해결 코드를 R로 작성한다.`

### `2-1 복사본 데이터를 이용하여 cty는 city로 hwy는 highway로 변수명을 수정하라.`

```R
mpg_new <- mpg %>%
  rename("city"="cty", "highway" = "hwy")

```



### `2-2 데이터 일부를 출력해서 변수명이 바뀌었는지 확인하라.`

```R
#2-2
head(mpg_new)
```





### `3-1 ggplot2의 midwest 데이터를 데이터 프레임 형태로 불러와서 데이터의 특성을 파악하세요.`

```R
midwest <- as.data.frame(midwest)
str(midwest)
```



### `3-2 poptotal(전체 인구)을 total로, popasian(아시아 인구)을 asian으로 변수명을 수정하세요.  `

```R
midwest_new <- midwest %>%
  rename("total"="poptotal", "asian" = "popasian")
head(midwest_new)
```



### `3-3 total, asian 변수를 이용해 '전체 인구 대비 아시아 인구 백분율' 파생변수를 만들어 보세요`

```R
#3-3
midwest_new %>%
  mutate(total_p_asian =  (asian/total) * 100) %>%  head   
```



### `3-4 아시아 인구 백분율 전체 평균을 구하고, 평균을 초과하면 "large", 그 외에는 "small"을 부여하는 파생변수를 만들어 보세요. `

``` R
#3-4
midwest_new %>%
  mutate(total_p_asian =  (asian/total) * 100,
         avg = sum(total_p_asian)/length(total_p_asian),
         asian_avg = ifelse(total_p_asian > avg, "large", "small")) %>%
  head
```



### `4-1 자동차 배기량에 따라 고속도로 연비가 어떻게 다른지 알아보려고 한다. displ(배기량)이 4 이거나 5인 자동차의 hwy(고속도로 연비)의 평균을 구하라.`

``` R
#4-1
mpg %>%
  group_by(displ) %>%
  summarise(mean_hwy = mean(hwy)) %>%
  filter(displ == 4 | displ == 5)

```



### `4-2  자동차 제조 회사에 따라 도시 연비가 다른지 알아보려고 한다. "audi"와 "toyota"중에서 어느 manufacturer(자동차 제조 회사)의 cty(도시 연비)가 평균적으로 더 높은지 알아보라. `

```R
#4-2
mpg %>%
  group_by(manufacturer) %>% 
  summarise(mean_cty = mean(cty)) %>%
  filter(manufacturer == 'audi' | manufacturer =='toyota')

```



### `4-3 "chevrolet", "ford", "honda" 자동차의 고속도로 연비 평균을 알아보려고 한다. 이 회사들의 자동차를 추출한 뒤 hwy 전체 평균을 구하라.`

``` R
#4-3
mpg %>%
  group_by(manufacturer) %>% 
  filter(manufacturer == 'chevrolet' | manufacturer =='ford' | manufacturer == 'honda') %>% 
  summarise(mean = mean(hwy)) %>% 
  mutate (mean_cfh = mean(mean))

```



### `5-1 mpg 데이터의 일부만 추출하여 분석에 활용하려고 한다. class(자동차 종류), cty(도시 연비) 변수만을 추출하여 새로운 데이터를 만들고 확인하라.`

```R
#5-1
mympg <- mpg %>% select(class, cty)
head(mympg)

```



### `5-2  자동차의 종류에 따라 도시 연비가 다른지 알아보고자 한다. 5-1에서 추출한 데이터를 class가 "suv"인 자동차와 "compact"인 자동차 중 어떤 자동차의 cty(도시 연비)가 높은지 비교하라.`

```R
#5-2
mympg %>%
  group_by(class) %>% 
  filter(class == 'suv' | class == 'compact') %>% 
  summarise(city_mean = mean(cty))

```



### `6-1 "audi" 에서 생산한 자동차 중 hwy가 1-5위에 해당하는 자동차의 데이터를 출력하라.`

``` R
mpg %>%
  filter(manufacturer == 'audi') %>%
  arrange(desc(hwy)) %>% 
  head(5) 
```

