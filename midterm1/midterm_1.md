---
title: "Midterm 1"
author: "Eliza Mata"
date: "2022-01-27"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your code should be organized, clean, and run free from errors. Remember, you must remove the `#` for any included code chunks to run. Be sure to add your name to the author header above. You may use any resources to answer these questions (including each other), but you may not post questions to Open Stacks or external help sites. There are 15 total questions, each is worth 2 points.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

This exam is due by 12:00p on Thursday, January 27.  

## Load the tidyverse
If you plan to use any other libraries to complete this assignment then you should load them here.

```r
library(tidyverse)
```

```
## -- Attaching packages --------------------------------------- tidyverse 1.3.1 --
```

```
## v ggplot2 3.3.5     v purrr   0.3.4
## v tibble  3.1.6     v dplyr   1.0.7
## v tidyr   1.1.4     v stringr 1.4.0
## v readr   2.1.1     v forcats 0.5.1
```

```
## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```

```r
library(janitor)
```

```
## 
## Attaching package: 'janitor'
```

```
## The following objects are masked from 'package:stats':
## 
##     chisq.test, fisher.test
```

## Questions  
Wikipedia's definition of [data science](https://en.wikipedia.org/wiki/Data_science): "Data science is an interdisciplinary field that uses scientific methods, processes, algorithms and systems to extract knowledge and insights from noisy, structured and unstructured data, and apply knowledge and actionable insights from data across a broad range of application domains."  

1. (2 points) Consider the definition of data science above. Although we are only part-way through the quarter, what specific elements of data science do you feel we have practiced? Provide at least one specific example.  
  * **We have used systems in order to extract information from the data we used in our home works and labs. We have also cleaned numbers that are structured in order to have better clarity on what the data represents.**

2. (2 points) What is the most helpful or interesting thing you have learned so far in BIS 15L? What is something that you think needs more work or practice?  
 * **I learned that even professionally collected data will have some mistakes that need to be fixed, unfortunately. I need more overall practice to get more comfortable with using functions.**

In the midterm 1 folder there is a second folder called `data`. Inside the `data` folder, there is a .csv file called `ElephantsMF`. These data are from Phyllis Lee, Stirling University, and are related to Lee, P., et al. (2013), "Enduring consequences of early experiences: 40-year effects on survival and success among African elephants (Loxodonta africana)," Biology Letters, 9: 20130011. [kaggle](https://www.kaggle.com/mostafaelseidy/elephantsmf).  

3. (2 points) Please load these data as a new object called `elephants`. Use the function(s) of your choice to get an idea of the structure of the data. Be sure to show the class of each variable.

```r
elephants<-readr::read_csv("data/ElephantsMF.csv")
```

```
## Rows: 288 Columns: 3
```

```
## -- Column specification --------------------------------------------------------
## Delimiter: ","
## chr (1): Sex
## dbl (2): Age, Height
```

```
## 
## i Use `spec()` to retrieve the full column specification for this data.
## i Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

4. (2 points) Change the names of the variables to lower case and change the class of the variable `sex` to a factor.

```r
elephants<-clean_names(elephants)
```

```r
elephants$sex<-as.factor(elephants$sex)
is.factor(elephants$sex)
```

```
## [1] TRUE
```

5. (2 points) How many male and female elephants are represented in the data?

```r
elephants %>%
  count(sex, sort=T)
```

```
## # A tibble: 2 x 2
##   sex       n
##   <fct> <int>
## 1 F       150
## 2 M       138
```
 * **There are 150 females and 138 males**
 
6. (2 points) What is the average age all elephants in the data?

```r
  mean(elephants$age)
```

```
## [1] 10.97132
```
* **10.97132**

7. (2 points) How does the average age and height of elephants compare by sex?

```r
male_elephants<-elephants %>%
  filter(sex=="M")
```

```r
female_elephants<-elephants%>%
  filter(sex=="F")
```

```r
female_elephants %>%
  summarize(average_age=mean(age),average_height=mean(height))
```

```
## # A tibble: 1 x 2
##   average_age average_height
##         <dbl>          <dbl>
## 1        12.8           190.
```

```r
male_elephants %>%
  summarize(average_age=mean(age), average_height=mean(height))
```

```
## # A tibble: 1 x 2
##   average_age average_height
##         <dbl>          <dbl>
## 1        8.95           185.
```

8. (2 points) How does the average height of elephants compare by sex for individuals over 20 years old. Include the min and max height as well as the number of individuals in the sample as part of your analysis.  

```r
female_elephants %>%
  filter(age>20) %>%
  summarize(average_height=mean(height), min_height=min(height),max_height=max(height), total=n())
```

```
## # A tibble: 1 x 4
##   average_height min_height max_height total
##            <dbl>      <dbl>      <dbl> <int>
## 1           232.       193.       278.    37
```

```r
male_elephants %>%
  filter(age>20) %>%
  summarize(average_height=mean(height), min_height=min(height),max_height=max(height), total=n())
```

```
## # A tibble: 1 x 4
##   average_height min_height max_height total
##            <dbl>      <dbl>      <dbl> <int>
## 1           270.       229.       304.    13
```

For the next series of questions, we will use data from a study on vertebrate community composition and impacts from defaunation in [Gabon, Africa](https://en.wikipedia.org/wiki/Gabon). One thing to notice is that the data include 24 separate transects. Each transect represents a path through different forest management areas.  

Reference: Koerner SE, Poulsen JR, Blanchard EJ, Okouyi J, Clark CJ. Vertebrate community composition and diversity declines along a defaunation gradient radiating from rural villages in Gabon. _Journal of Applied Ecology_. 2016. This paper, along with a description of the variables is included inside the midterm 1 folder.  

9. (2 points) Load `IvindoData_DryadVersion.csv` and use the function(s) of your choice to get an idea of the overall structure. Change the variables `HuntCat` and `LandUse` to factors.

```r
defaunation<-readr::read_csv("data/IvindoData_DryadVersion.csv")
```

```
## Rows: 24 Columns: 26
```

```
## -- Column specification --------------------------------------------------------
## Delimiter: ","
## chr  (2): HuntCat, LandUse
## dbl (24): TransectID, Distance, NumHouseholds, Veg_Rich, Veg_Stems, Veg_lian...
```

```
## 
## i Use `spec()` to retrieve the full column specification for this data.
## i Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
defaunation<-clean_names(defaunation)
```

10. (4 points) For the transects with high and moderate hunting intensity, how does the average diversity of birds and mammals compare?

```r
defaunation %>% 
  select(hunt_cat,diversity_bird_species, diversity_mammal_species) %>%
  filter(hunt_cat=="High"|hunt_cat=="Moderate") %>%
  mutate(average_bird_diversity=mean(diversity_bird_species), average_mammal_diversity=mean(diversity_mammal_species))
```

```
## # A tibble: 15 x 5
##    hunt_cat diversity_bird_s~ diversity_mamma~ average_bird_di~ average_mammal_~
##    <chr>                <dbl>            <dbl>            <dbl>            <dbl>
##  1 Moderate              1.76             1.76             1.64             1.71
##  2 High                  1.88             1.71             1.64             1.71
##  3 High                  1.26             1.80             1.64             1.71
##  4 Moderate              1.60             1.69             1.64             1.71
##  5 Moderate              1.68             2.06             1.64             1.71
##  6 High                  1.71             1.57             1.64             1.71
##  7 Moderate              1.46             1.44             1.64             1.71
##  8 High                  1.86             1.64             1.64             1.71
##  9 Moderate              1.60             1.38             1.64             1.71
## 10 Moderate              1.71             1.51             1.64             1.71
## 11 High                  1.81             1.71             1.64             1.71
## 12 High                  1.39             1.90             1.64             1.71
## 13 Moderate              1.48             1.94             1.64             1.71
## 14 Moderate              1.68             1.68             1.64             1.71
## 15 High                  1.72             1.83             1.64             1.71
```

11. (4 points) One of the conclusions in the study is that the relative abundance of animals drops off the closer you get to a village. Let's try to reconstruct this (without the statistics). How does the relative abundance (RA) of apes, birds, elephants, monkeys, rodents, and ungulates compare between sites that are less than 3km from a village to sites that are greater than 25km from a village? The variable `Distance` measures the distance of the transect from the nearest village. Hint: try using the `across` operator.  

```r
defaunation %>%
  select(distance,contains("ra")) %>%
 arrange(desc(distance)) %>%
  filter(distance<3|distance>25)
```

```
## # A tibble: 3 x 8
##   distance transect_id ra_apes ra_birds ra_elephant ra_monkeys ra_rodent
##      <dbl>       <dbl>   <dbl>    <dbl>       <dbl>      <dbl>     <dbl>
## 1    26.8           24    4.91     31.6        0         54.1       1.29
## 2     2.92          27    0.24     68.2        0         25.6       4.05
## 3     2.7           15    0        85.0        0.29       9.09      3.74
## # ... with 1 more variable: ra_ungulate <dbl>
```

12. (4 points) Based on your interest, do one exploratory analysis on the `gabon` data of your choice. This analysis needs to include a minimum of two functions in `dplyr.`

```r
land_use_diversity<-defaunation %>% 
  group_by(land_use) %>%
  select(land_use,contains("ra"))
land_use_diversity
```

```
## # A tibble: 24 x 8
## # Groups:   land_use [3]
##    land_use transect_id ra_apes ra_birds ra_elephant ra_monkeys ra_rodent
##    <chr>          <dbl>   <dbl>    <dbl>       <dbl>      <dbl>     <dbl>
##  1 Park               1    1.87     52.7        0         38.6       4.22
##  2 Park               2    0        52.2        0.86      28.5       6.04
##  3 Park               2    4.49     37.4        1.33      41.8       1.06
##  4 Logging            3   12.9      59.3        0.56      19.8       3.66
##  5 Park               4    0        52.6        1         41.3       2.52
##  6 Park               5    2.48     38.6        0         43.3       1.83
##  7 Park               6    3.78     42.7        1.11      46.2       3.1 
##  8 Logging            7    6.17     33.8        0.43      49.5       1.26
##  9 Neither            8    0        73.1        2.2       20.0       4.37
## 10 Logging            9    0        85.0        0          5.84      6.31
## # ... with 14 more rows, and 1 more variable: ra_ungulate <dbl>
```

```r
land_use_diversity %>%
  summarize(average_ra_apes=mean(ra_apes), average_ra_birds=mean(ra_birds),average_ra_elephant=mean(ra_elephant), average_ra_monkeys=mean(ra_monkeys), average_ra_rodent=mean(ra_rodent), average_ra_ungulate=mean(ra_ungulate))   
```

```
## # A tibble: 3 x 7
##   land_use average_ra_apes average_ra_birds average_ra_elephant average_ra_monk~
##   <chr>              <dbl>            <dbl>               <dbl>            <dbl>
## 1 Logging             2.10             62.7               0.425             28.4
## 2 Neither             1.05             71.0               0.815             22.1
## 3 Park                2.50             44.0               0.614             42.0
## # ... with 2 more variables: average_ra_rodent <dbl>, average_ra_ungulate <dbl>
```

