## day 20: dplyr package

### `1. mpg 데이터 복사본을 만들고 cty와 hwy를 더한 "합산 연비 변수"를 추가하라.`

``` R
library(dplyr)
library(ggplot2)

mpg <- as.data.frame(mpg)
head(mpg)

mympg1 <- mpg
head(mympg1)
mympg1 %>% 
  mutate(total_hwycty = hwy+cty) %>% head
```



### `2. 앞에서 만든 "합산 연비 변수"를 2로 나누어 "평균 연비 변수"를 추가하라.`

```R
mympg1 %>% 
  mutate(total_hwycty = hwy+cty,
         mean_hwycty = total_hwycty/2) %>% head
```



### `3. "평균 연비 변수"가 가장 높은 자동차 3종의 데이터를 출력하라.`

```R
mympg1 %>% 
  mutate(total_hwycty = hwy+cty,
         mean_hwycty = total_hwycty/2) %>%
  arrange(desc(mean_hwycty)) %>% head(3)
```



### `4. 위의 1~3번 문제를 해결할 수 있는 하나로 연결된 dplyr 구문을 만들어 출력하라. 데이터는 복사본 대신 mpg 원본을 사용하라.`

```R
mpg %>% 
  mutate(total_hwycty = hwy+cty,
         mean_hwycty = total_hwycty/2) %>%
  arrange(desc(mean_hwycty)) %>% head(3)
```



### `5. mpg 데이터의 class는 "suv", "compact" 등 자동차를 특징에 따라 일곱 종류로 분류한 변수이다. 어떤 차종의 연비가 높은지 비교하려고 할 때 class 별 cty의 평균을 구하시오.`

```R
mpg %>% group_by(class) %>%
  summarise(mean = mean(hwy)) %>%  head
```



### `6. 앞 문제의 출력 결과는 class 값 알파벳 순으로 정렬되어 있다. 어떤 차종의 도시 연비가 높은지 쉽게 알아볼 수 있도록 cty 평균이 높은 순으로 정렬해 출력하라.`

```R
mpg %>% group_by(class) %>%
  summarise(mean = mean(hwy)) %>%
  arrange(desc(mean)) %>% head
```



### `7. 어떤 회사 자동차의 hwy(고속도로 연비)가 가장 높은지 알아보려고 한다. hwy 평균이 가장 높은 회사 세 곳을 출력하시오.`

``` R
#8-2
mpg %>% group_by(class) %>%
  summarise(mean = mean(hwy)) %>%
  arrange(desc(mean)) %>% head
```



### `8. 어떤 회사에서 "compact(경차)" 차종을 가장 많이 생산하는지 알아보려고 한다. 각 회사별 "compact" 차종 수를 내림차순으로 정렬해 출력하라.`

``` R
mpg %>% group_by(manufacturer) %>%
  summarise(mean = mean(hwy)) %>%
  arrange(desc(mean)) %>%
  head(3) 

```



### `9. mpg 데이터의 fl 변수는 자동차에 사용하는 연료(fuel)를 의미한다. 아래는 자동차 연료별 가격을 나타낸 표이다. 정보를 이용하여 연료와 가격으로 구성된 데이터 프레임을 생성하라.`

``` R

fuel <- data.frame(fl = c("c", "d", "e", "p", "r"),
                   price_fl = c(2.35, 2.38, 2.11, 2.76, 2.22),
                   stringsAsFactors = F)
fuel


```



### `10. mpg 데이터에는 연료 종류를 나타낸 fl 변수는 있지만 연료 가격을 나타낸 변수는 없다. 위에서 만든 fuel 데이터를 이용해서 mpg 데이터에 price_fl(연료 가격) 변수를 추가하라.`

``` R
mympg2 <- full_join(mpg, fuel, by = "fl") 
#head(mympg2)

mympg2 %>% select(model, fl, price_fl) %>% head(5)

```



### 아래 11~14번 문제는 ggplot2 패키지의 midwest 데이터를 이용한다.



### `11. popadults는 해당 지역 성인 인구, poptotal은 전체 인구를 나타낸다. midwest 데이터에 "전체 인구 대비 미성년 인구 백분율" 변수를 추가하라.`

``` R
midwest %>%
  mutate(total_p_adults =  ((poptotal-popadults)/poptotal) * 100) %>%  head
```



### `12. 미성년 인구 백분율이 가장 높은 상위 5개 county(지역)의 미성년 인구 백분율을 출력하라.`

``` R
midwest %>%
  mutate(total_p_adults =  ((poptotal-popadults)/poptotal) * 100) %>%
  arrange(desc(total_p_adults)) %>%
  head(5) %>%
  select(county, total_p_adults)

```



### `13. 분류표의 기준에 따라 미성년 비율 등급 변수를 추가하고, 각 등급에 몇 개의 지역이 있는지 알아보시오.`

``` R
midwest %>%
  mutate(total_p_adults =  ((poptotal-popadults)/poptotal) * 100,
         grade_underage = ifelse(total_p_adults >= 40, "large", 
                                 ifelse(total_p_adults >= 30, "middle", "small"))) %>%
  count(grade_underage)
```



### `14. popasian은 해당 지역 아시아인 인구를 나타냅니다. "전체 인구 대비 아시아인 인구 백분율" 변수를 추가하고 하위 10개 지역의 state(주), county(지역명), 아시아인 인구 백분율을 출력하세요.`

``` R
midwest %>%
  mutate(total_p_asian =  (popasian/poptotal) * 100) %>%
  arrange(total_p_asian) %>% head(10) %>%
  select(state, county, total_p_asian)  
```



### `15. mpg 데이터 원본에는 결측치가 존재하지 않는다. mpg 데이터를 불러와 몇 개의 값을 결측치로 만든다. 아래 코드를 실행하면 다섯 행의 hwy 변수에 NA가 할당된다.`

```R
mpg <- as.data.frame(ggplot2::mpg)
mpg[c(65, 124, 131, 153, 212), "hwy"] <- NA
```



### `drv(구동 방식) 별로 hwy(고속도로 연비) 평균이 어떻게 다른지 알아보려고 한다. 분석을 하기 전에 두 변수에 결측치가 있는지 확인하라.`

``` R
table(is.na(mpg$hwy)) # 5개
table(is.na(mpg$drv)) # 없음
```



### `16. filter()를 이용하여 hwy 변수의 결측치를 제외하고, 어떤 구동방식의 hwy 평균이 높은지 알아보라. 하나의 dplyr 구문으로 만들어야 한다.`

``` R
mpg %>% filter(is.na(hwy))  

mpg %>%
  filter(!is.na(hwy)) %>%
  group_by(drv) %>% 
  summarise(mean = mean(hwy)) %>% 
  arrange(desc(mean)) %>%
  head(1) %>%
  select(drv)
```



### `17. mpg 데이터에 아래와 같이 이상치를 만든다. drv(구동방식) 변수의 값은 4(사륜구동), f(전륜구동), r(후륜구동) 세 종류로 되어있다. 몇 개의 행에 존재할 수 없는 값 k를 할당한다. cty(도시 연비) 변수도 몇 개의 행에 극단적으로 크거나 작은 값을 할당한다.`

### `drv에 이상치가 있는지 확인하라. 이상치를 결측 처리한 다음 이상치가 사라졌는지까지 확인하라. 결측치 처리할 때는 %in% 기호를 활용하라.`

``` R
mpg <- as.data.frame(ggplot2::mpg)
mpg[c(10, 14, 58, 93), "drv"] <- "k"
mpg[c(29, 43, 129, 203), "cty"] <- c(3, 4, 39, 42)

table(mpg$drv)
mpg$drv <- ifelse(mpg$drv %in% 'k', NA, mpg$drv)
table(mpg$drv) # 제거완료
```



### `18. 상자 그림을 이용하여 cty에 이상치가 있는지 확인하라. 상자 그림의 통계치를 이용해 정상 범위를 벗어난 값을 결측 처리한 후 다시 상자 그림을 만들어 이상치가 사라졌는지 확인하라.`

``` R
boxplot(mpg$cty)
boxplot(mpg$cty)$stats 
mpg$cty <- ifelse(mpg$cty < 9 | mpg$cty > 26, NA, mpg$cty)
table(is.na(mpg$cty))

boxplot(mpg$cty) # 결측치제거 완료
```



### `19. 두 변수의 이상치를 결측처리 했으니 이제 분석할 차례입니다. 이상치를 제외한 다음 drv 별로 cty 평균이 어떻게 다른지 알아보시오. 하나의 dplyr 구문으로 만들어야 한다.`

```R
mpg %>%
  group_by(drv) %>%
  summarise(mean_cty = mean(cty, na.rm = T))
```

