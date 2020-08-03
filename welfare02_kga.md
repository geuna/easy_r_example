성별에 따른 월급 차이 분석하기
================
김근아
July 31, 2020

## 2\. 성별에 따른 월급 차이 - 성별에 따라 월급이 다를까?

### 데이터 분석 절차

#### 1\. 변수 검토하기

``` r
class(welfare$sex)

table(welfare$sex)
```

#### 2\. 전처리

``` r
# 결측치 확인
table(is.na(welfare$sex))

# 성별 항목 이름 부여
welfare$sex <- ifelse(welfare$sex == 1, "male", "female")

# 변수 검토 및 전처리
class(welfare$income)

summary(welfare$income)

qplot(welfare$income)
```

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

    ## Warning: Removed 12030 rows containing non-finite values (stat_bin).

![](welfare02_kga_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

``` r
# 이상치 결측 처리
welfare$income <- ifelse(welfare$income %in% c(0,9999), NA, welfare$income)

table(is.na(welfare$income))
```

### 성별에 따른 월급 차이 분석하기

#### 1\. 성별 월급 평균표 만들기

``` r
sex_income <- welfare %>% 
  filter(!is.na(income)) %>% 
  group_by(sex) %>% 
  summarise(mean_income = mean(income))
```

    ## `summarise()` ungrouping output (override with `.groups` argument)

``` r
sex_income
```

#### 2\. 그래프 만들기

``` r
ggplot(data=sex_income, aes(x= sex, y=mean_income)) + geom_col()
```

![](welfare02_kga_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->
