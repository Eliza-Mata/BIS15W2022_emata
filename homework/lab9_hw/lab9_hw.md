---
title: "Lab 9 Homework"
author: "Eliza Mata"
date: "2022-03-14"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the libraries

```r
library(tidyverse)
library(janitor)
library(here)
library(naniar)
```

For this homework, we will take a departure from biological data and use data about California colleges. These data are a subset of the national college scorecard (https://collegescorecard.ed.gov/data/). Load the `ca_college_data.csv` as a new object called `colleges`.

```r
colleges<-read.csv("data/ca_college_data.csv")
```

The variables are a bit hard to decipher, here is a key:  

INSTNM: Institution name  
CITY: California city  
STABBR: Location state  
ZIP: Zip code  
ADM_RATE: Admission rate  
SAT_AVG: SAT average score  
PCIP26: Percentage of degrees awarded in Biological And Biomedical Sciences  
COSTT4_A: Annual cost of attendance  
C150_4_POOLED: 4-year completion rate  
PFTFTUG1_EF: Percentage of undergraduate students who are first-time, full-time degree/certificate-seeking undergraduate students  

1. Use your preferred function(s) to have a look at the data and get an idea of its structure. Make sure you summarize NA's and determine whether or not the data are tidy. You may also consider dealing with any naming issues.

```r
colleges<-clean_names(colleges)
```




```r
summary(colleges)
```

```
##     instnm              city              stabbr              zip           
##  Length:341         Length:341         Length:341         Length:341        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##     adm_rate         sat_avg         pcip26           costt4_a    
##  Min.   :0.0807   Min.   : 870   Min.   :0.00000   Min.   : 7956  
##  1st Qu.:0.4581   1st Qu.: 985   1st Qu.:0.00000   1st Qu.:12578  
##  Median :0.6370   Median :1078   Median :0.00000   Median :16591  
##  Mean   :0.5901   Mean   :1112   Mean   :0.01981   Mean   :26685  
##  3rd Qu.:0.7461   3rd Qu.:1237   3rd Qu.:0.02457   3rd Qu.:39289  
##  Max.   :1.0000   Max.   :1555   Max.   :0.21650   Max.   :69355  
##  NA's   :240      NA's   :276    NA's   :35        NA's   :124    
##  c150_4_pooled     pftftug1_ef    
##  Min.   :0.0625   Min.   :0.0064  
##  1st Qu.:0.4265   1st Qu.:0.3212  
##  Median :0.5845   Median :0.5016  
##  Mean   :0.5705   Mean   :0.5577  
##  3rd Qu.:0.7162   3rd Qu.:0.8117  
##  Max.   :0.9569   Max.   :1.0000  
##  NA's   :221      NA's   :53
```

2. Which cities in California have the highest number of colleges?

```r
college_cities<-colleges %>%
 count(city) %>%
  arrange(desc(n)) %>%
   head(10) 
```
 * **Los Angeles**

3. Based on your answer to #2, make a plot that shows the number of colleges in the top 10 cities.

```r
college_cities %>%
  ggplot(aes(x=city, y=n)) + geom_col()
```

![](lab9_hw_files/figure-html/unnamed-chunk-7-1.png)<!-- -->



4. The column `COSTT4_A` is the annual cost of each institution. Which city has the highest average cost? Where is it located?

```r
colleges %>%
  select(city, costt4_a) %>%
  filter(costt4_a!="NA") %>%
  group_by(city) %>%
  summarise("avr_cost" = mean(costt4_a)) %>%
  arrange(desc(avr_cost))
```

```
## # A tibble: 132 x 2
##    city                avr_cost
##    <chr>                  <dbl>
##  1 Claremont              66498
##  2 Malibu                 66152
##  3 Valencia               64686
##  4 Orange                 64501
##  5 Redlands               61542
##  6 Moraga                 61095
##  7 Atherton               56035
##  8 Thousand Oaks          54373
##  9 Rancho Palos Verdes    50758
## 10 La Verne               50603
## # ... with 122 more rows
```

 * **Claremont CA**
5. Based on your answer to #4, make a plot that compares the cost of the individual colleges in the most expensive city. Bonus! Add UC Davis here to see how it compares :>).

```r
colleges %>%
  filter(city=="Claremont") %>%
  filter(costt4_a!="NA") %>%
  ggplot(aes(x=instnm,y=costt4_a))+geom_col()
```

![](lab9_hw_files/figure-html/unnamed-chunk-9-1.png)<!-- -->

6. The column `ADM_RATE` is the admissions rate by college and `C150_4_POOLED` is the four-year completion rate. Use a scatterplot to show the relationship between these two variables. What do you think this means?

```r
colleges %>%
  ggplot(aes(x=c150_4_pooled, y=adm_rate))+geom_point()
```

```
## Warning: Removed 251 rows containing missing values (geom_point).
```

![](lab9_hw_files/figure-html/unnamed-chunk-10-1.png)<!-- -->

7. Is there a relationship between cost and four-year completion rate? (You don't need to do the stats, just produce a plot). What do you think this means?

```r
colleges %>%
  ggplot(aes(x=costt4_a, y=c150_4_pooled))+geom_point()
```

```
## Warning: Removed 225 rows containing missing values (geom_point).
```

![](lab9_hw_files/figure-html/unnamed-chunk-11-1.png)<!-- -->

8. The column titled `INSTNM` is the institution name. We are only interested in the University of California colleges. Make a new data frame that is restricted to UC institutions. You can remove `Hastings College of Law` and `UC San Francisco` as we are only interested in undergraduate institutions.

```r
uc_colleges<-colleges%>%
  arrange(desc(instnm)) %>%
  slice(24:33) %>%
  filter(instnm!="University of California-Hastings College of Law")%>%
  filter(instnm!="University of California-San Francisco")
```

Remove `Hastings College of Law` and `UC San Francisco` and store the final data frame as a new object `univ_calif_final`.

```r
univ_calif_final<-uc_colleges
```

Use `separate()` to separate institution name into two new columns "UNIV" and "CAMPUS".

```r
univ_calif_final<- univ_calif_final %>%
  separate(instnm, into = c("univ", "campus"), sep="-" )
```

9. The column `ADM_RATE` is the admissions rate by campus. Which UC has the lowest and highest admissions rates? Produce a numerical summary and an appropriate plot.

```r
univ_calif_final %>%
  group_by(campus) %>%
  arrange(adm_rate)
```

```
## # A tibble: 8 x 11
## # Groups:   campus [8]
##   univ  campus city  stabbr zip   adm_rate sat_avg pcip26 costt4_a c150_4_pooled
##   <chr> <chr>  <chr> <chr>  <chr>    <dbl>   <int>  <dbl>    <int>         <dbl>
## 1 Univ~ Berke~ Berk~ CA     94720    0.169    1422  0.105    34924         0.916
## 2 Univ~ Los A~ Los ~ CA     9009~    0.180    1334  0.155    33078         0.911
## 3 Univ~ San D~ La J~ CA     92093    0.357    1324  0.216    31043         0.872
## 4 Univ~ Santa~ Sant~ CA     93106    0.358    1281  0.108    34998         0.816
## 5 Univ~ Irvine Irvi~ CA     92697    0.406    1206  0.107    31198         0.876
## 6 Univ~ Davis  Davis CA     9561~    0.423    1218  0.198    33904         0.850
## 7 Univ~ Santa~ Sant~ CA     9506~    0.578    1201  0.193    34608         0.776
## 8 Univ~ River~ Rive~ CA     92521    0.663    1078  0.149    31494         0.73 
## # ... with 1 more variable: pftftug1_ef <dbl>
```



10. If you wanted to get a degree in biological or biomedical sciences, which campus confers the majority of these degrees? Produce a numerical summary and an appropriate plot.

```r
univ_bio<-colleges %>%
  select(instnm,pcip26) %>%
  arrange(desc(pcip26)) %>%
  head(5)
univ_bio
```

```
##                                 instnm pcip26
## 1   University of California-San Diego 0.2165
## 2       University of California-Davis 0.1975
## 3  University of California-Santa Cruz 0.1927
## 4                       Pomona College 0.1711
## 5 University of California-Los Angeles 0.1548
```


```r
univ_bio %>%
  ggplot(aes(x=instnm, y=pcip26))+geom_col()
```

![](lab9_hw_files/figure-html/unnamed-chunk-18-1.png)<!-- -->

## Knit Your Output and Post to [GitHub](https://github.com/FRS417-DataScienceBiologists)
