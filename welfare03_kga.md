나이와 월급의 관계 - 몇 살 때 월급을 가장 많이 받을까?
================
김근아
July 31, 2020

## 2\. 성별에 따른 월급 차이 - 성별에 따라 월급이 다를까?

### 데이터 분석 절차

#### 1\. 변수 검토하기

``` r
class(welfare$birth)

summary(welfare$birth)

qplot(welfare$birth)
```

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](welfare03_kga_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

#### 2\. 전처리

``` r
# 이상치 확인
summary(welfare$birth)

# 결측치 확인
table(is.na(welfare$birth))
```

### 나이와 월급의 관계 분석하기

#### 1\. 나이에 따른 월급 평균표 만들기

``` r
age_income <- welfare %>% 
  filter(!is.na(income)) %>% 
  group_by(age) %>% 
  summarise(mean_income = mean(income))
```

    ## `summarise()` ungrouping output (override with `.groups` argument)

``` r
age_income
```

#### 2\. 그래프 만들기

``` r
ggplot(data=age_income, aes(x= age, y=mean_income)) + geom_line()
```

![](welfare03_kga_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->
