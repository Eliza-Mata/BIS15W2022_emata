---
title: "Homework 1"
author: "Eliza Mata"
output: 
  html_document: 
    keep_md: yes
---



## Homework Q&A
**1.What is the difference between R and RStudio? What is GitHub and why is it useful to programmers?** 
   
   R is a scripting language, while Rstudio is a GUI that needs R to function.
    
  GitHub is a file storage and management [website](https://github.com/) and desktop application that can use and store code. It is useful to programmers because it can directly be manipulated with different code.

**2.Calculate the following expressions. Be sure to include each one in a separate code chunk.**


```r
+5-3*2
```

```
## [1] -1
```

```r
+8/2**2
```

```
## [1] 2
```
**3.Did any of the results in #2 surprise you? Write two programs that calculate each expression such that the result for the first example is 4 and the second example is 16.**

    No. 

```r
(3*8)/6
```

```
## [1] 4
```

```r
2*2*2*2
```

```
## [1] 16
```
**4. Objects in R are a way in which we can store data or operations. We will talk more about objects next week. For now, make a new object pi as 3.14159265359 by running the following code chunk. You should now see the object pi in the environment window in the top right.**

```r
pi <- 3.14159265359
```
**5. Let's say we want to multiply `pi` by 2. Using the same arithmetic principles that we just learned, write a code chunk that performs this operation using the object we created.**  


```r
pi*2
```

```
## [1] 6.283185
```
**6. In order to get help with any command in R, just type a `?` in front the command of interest. Practice this by running the following code chunk.**  

```r
?mean
```

```
## starting httpd help server ... done
```

**7. Let's calculate the mean for the numbers 2, 8, 6, 4, 9, 10. I have built an object `x` for you below so all you need to do is run the first code chunk and then create a second code chunk that shows the calculation. Give it a try!**  

```r
x <- c(2, 8, 6, 6, 7, 4, 9, 9, 9, 10)
```
**8. Repeat the procedure above, but this time calculate the median.**  

```r
median(x)
```

```
## [1] 7.5
```

##Note: I might've misunderstood what we were supposed to do so I made a new file for our hw my bad :( 
