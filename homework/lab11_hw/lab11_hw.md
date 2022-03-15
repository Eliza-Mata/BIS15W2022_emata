---
title: "Lab 11 Homework"
author: "Eliza Mata"
date: "2022-03-14"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above. For any included plots, make sure they are clearly labeled. You are free to use any plot type that you feel best communicates the results of your analysis.  

**In this homework, you should make use of the aesthetics you have learned. It's OK to be flashy!**

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the libraries

```r
library(tidyverse)
library(janitor)
library(here)
library(naniar)
library(RColorBrewer)
```

## Resources
The idea for this assignment came from [Rebecca Barter's](http://www.rebeccabarter.com/blog/2017-11-17-ggplot2_tutorial/) ggplot tutorial so if you get stuck this is a good place to have a look.  

## Gapminder
For this assignment, we are going to use the dataset [gapminder](https://cran.r-project.org/web/packages/gapminder/index.html). Gapminder includes information about economics, population, and life expectancy from countries all over the world. You will need to install it before use. This is the same data that we will use for midterm 2 so this is good practice.

```r
#install.packages("gapminder")
library("gapminder")
```

## Questions
The questions below are open-ended and have many possible solutions. Your approach should, where appropriate, include numerical summaries and visuals. Be creative; assume you are building an analysis that you would ultimately present to an audience of stakeholders. Feel free to try out different `geoms` if they more clearly present your results.  

**1. Use the function(s) of your choice to get an idea of the overall structure of the data frame, including its dimensions, column names, variable classes, etc. As part of this, determine how NA's are treated in the data.**  

```r
gapminder <- gapminder
```

```r
head(gapminder)
```

```
## # A tibble: 6 x 6
##   country     continent  year lifeExp      pop gdpPercap
##   <fct>       <fct>     <int>   <dbl>    <int>     <dbl>
## 1 Afghanistan Asia       1952    28.8  8425333      779.
## 2 Afghanistan Asia       1957    30.3  9240934      821.
## 3 Afghanistan Asia       1962    32.0 10267083      853.
## 4 Afghanistan Asia       1967    34.0 11537966      836.
## 5 Afghanistan Asia       1972    36.1 13079460      740.
## 6 Afghanistan Asia       1977    38.4 14880372      786.
```

```r
summary(gapminder)
```

```
##         country        continent        year         lifeExp     
##  Afghanistan:  12   Africa  :624   Min.   :1952   Min.   :23.60  
##  Albania    :  12   Americas:300   1st Qu.:1966   1st Qu.:48.20  
##  Algeria    :  12   Asia    :396   Median :1980   Median :60.71  
##  Angola     :  12   Europe  :360   Mean   :1980   Mean   :59.47  
##  Argentina  :  12   Oceania : 24   3rd Qu.:1993   3rd Qu.:70.85  
##  Australia  :  12                  Max.   :2007   Max.   :82.60  
##  (Other)    :1632                                                
##       pop              gdpPercap       
##  Min.   :6.001e+04   Min.   :   241.2  
##  1st Qu.:2.794e+06   1st Qu.:  1202.1  
##  Median :7.024e+06   Median :  3531.8  
##  Mean   :2.960e+07   Mean   :  7215.3  
##  3rd Qu.:1.959e+07   3rd Qu.:  9325.5  
##  Max.   :1.319e+09   Max.   :113523.1  
## 
```

```r
gapminder <-clean_names(gapminder)
```


**2. Among the interesting variables in gapminder is life expectancy. How has global life expectancy changed between 1952 and 2007?**

```r
gminder_1952 <- gapminder %>%
  filter(between(year, 1952, 2007))
gminder_1952
```

```
## # A tibble: 1,704 x 6
##    country     continent  year life_exp      pop gdp_percap
##    <fct>       <fct>     <int>    <dbl>    <int>      <dbl>
##  1 Afghanistan Asia       1952     28.8  8425333       779.
##  2 Afghanistan Asia       1957     30.3  9240934       821.
##  3 Afghanistan Asia       1962     32.0 10267083       853.
##  4 Afghanistan Asia       1967     34.0 11537966       836.
##  5 Afghanistan Asia       1972     36.1 13079460       740.
##  6 Afghanistan Asia       1977     38.4 14880372       786.
##  7 Afghanistan Asia       1982     39.9 12881816       978.
##  8 Afghanistan Asia       1987     40.8 13867957       852.
##  9 Afghanistan Asia       1992     41.7 16317921       649.
## 10 Afghanistan Asia       1997     41.8 22227415       635.
## # ... with 1,694 more rows
```


```r
gminder_1952 %>%
  group_by(country) %>%
  summarise(life_exp_growth = max(life_exp)- min(life_exp)) %>%
  arrange(desc(life_exp_growth))
```

```
## # A tibble: 142 x 2
##    country            life_exp_growth
##    <fct>                        <dbl>
##  1 Oman                          38.1
##  2 Vietnam                       33.8
##  3 Indonesia                     33.2
##  4 Saudi Arabia                  32.9
##  5 Libya                         31.2
##  6 Korea, Rep.                   31.2
##  7 Nicaragua                     30.6
##  8 West Bank and Gaza            30.3
##  9 Yemen, Rep.                   30.2
## 10 Gambia                        29.4
## # ... with 132 more rows
```

**3. How do the distributions of life expectancy compare for the years 1952 and 2007?**

```r
gapminder%>%
  filter(year==1952) %>%
  ggplot( aes(x=life_exp))+
   geom_histogram(aes(y = ..density..), fill = "deepskyblue4", alpha = 0.4, color = "black")+
  geom_density(color = "red")
```

```
## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
```

![](lab11_hw_files/figure-html/unnamed-chunk-9-1.png)<!-- -->

```r
gapminder%>%
  filter(year==2007) %>%
  ggplot( aes(x=life_exp))+
   geom_histogram(aes(y = ..density..), fill = "deepskyblue4", alpha = 0.4, color = "black")+
  geom_density(color = "red")
```

```
## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
```

![](lab11_hw_files/figure-html/unnamed-chunk-10-1.png)<!-- -->

**4. Your answer above doesn't tell the whole story since life expectancy varies by region. Make a summary that shows the min, mean, and max life expectancy by continent for all years represented in the data.**

```r
a<- gapminder %>%
  group_by(continent, year ) %>%
  summarise(min_life_exp= min(life_exp), mean_life_exp = mean(life_exp), max_life_exp = max(life_exp) )
```

```
## `summarise()` has grouped output by 'continent'. You can override using the
## `.groups` argument.
```

```r
a
```

```
## # A tibble: 60 x 5
## # Groups:   continent [5]
##    continent  year min_life_exp mean_life_exp max_life_exp
##    <fct>     <int>        <dbl>         <dbl>        <dbl>
##  1 Africa     1952         30            39.1         52.7
##  2 Africa     1957         31.6          41.3         58.1
##  3 Africa     1962         32.8          43.3         60.2
##  4 Africa     1967         34.1          45.3         61.6
##  5 Africa     1972         35.4          47.5         64.3
##  6 Africa     1977         36.8          49.6         67.1
##  7 Africa     1982         38.4          51.6         69.9
##  8 Africa     1987         39.9          53.3         71.9
##  9 Africa     1992         23.6          53.6         73.6
## 10 Africa     1997         36.1          53.6         74.8
## # ... with 50 more rows
```

**5. How has life expectancy changed between 1952-2007 for each continent?**

```r
a %>%
  group_by(continent, year) %>%
  summarise( life_exp_change = max_life_exp - min_life_exp)
```

```
## `summarise()` has grouped output by 'continent'. You can override using the
## `.groups` argument.
```

```
## # A tibble: 60 x 3
## # Groups:   continent [5]
##    continent  year life_exp_change
##    <fct>     <int>           <dbl>
##  1 Africa     1952            22.7
##  2 Africa     1957            26.5
##  3 Africa     1962            27.5
##  4 Africa     1967            27.4
##  5 Africa     1972            28.9
##  6 Africa     1977            30.3
##  7 Africa     1982            31.4
##  8 Africa     1987            32.0
##  9 Africa     1992            50.0
## 10 Africa     1997            38.7
## # ... with 50 more rows
```

**6. We are interested in the relationship between per capita GDP and life expectancy; i.e. does having more money help you live longer?**

```r
gapminder %>%
  ggplot( aes(x= life_exp, y= gdp_percap)) +
  geom_point()
```

![](lab11_hw_files/figure-html/unnamed-chunk-13-1.png)<!-- -->

**7. Which countries have had the largest population growth since 1952?**

```r
b <- gminder_1952 %>%
  group_by(country) %>%
  summarise( life_exp_change = max(life_exp) - min(life_exp)) %>%
  arrange(desc(life_exp_change))
b
```

```
## # A tibble: 142 x 2
##    country            life_exp_change
##    <fct>                        <dbl>
##  1 Oman                          38.1
##  2 Vietnam                       33.8
##  3 Indonesia                     33.2
##  4 Saudi Arabia                  32.9
##  5 Libya                         31.2
##  6 Korea, Rep.                   31.2
##  7 Nicaragua                     30.6
##  8 West Bank and Gaza            30.3
##  9 Yemen, Rep.                   30.2
## 10 Gambia                        29.4
## # ... with 132 more rows
```


**8. Use your results from the question above to plot population growth for the top five countries since 1952.**

```r
gapminder %>%
  filter(country %in% c("Oman","Vietnam", "Indonesia","Saudi Arabia", "Libya" )) %>%
  ggplot(aes(x=year, y=life_exp, fill=country ))+
  geom_point()+ scale_colour_brewer(palette = "BuPu")
```

![](lab11_hw_files/figure-html/unnamed-chunk-15-1.png)<!-- -->

**9. How does per-capita GDP growth compare between these same five countries?**

```r
gapminder %>%
  filter(country %in% c("Oman","Vietnam", "Indonesia","Saudi Arabia", "Libya" )) %>%
  ggplot(aes(x=year, y=gdp_percap, fill=country ))+
  geom_point()+ scale_colour_brewer(palette = "BuPu")
```

![](lab11_hw_files/figure-html/unnamed-chunk-16-1.png)<!-- -->

**10. Make one plot of your choice that uses faceting!**

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences. 
