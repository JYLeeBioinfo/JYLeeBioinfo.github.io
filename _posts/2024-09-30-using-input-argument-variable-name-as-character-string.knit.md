---
title: "Using input argument variable name as character string"
output:
  html_document: default
date: "2024-09-30"
---

# 1. How to change the variable name of input argument into character string.


```r
test_fn = function(x){
  deparse(substitute(x))
}
```

-   `substitute` function returns the unevaluated expression

-   Next, `deparse` function converts the expression returned by `substitute` into a character string.


```r
# Variable
a = 1
print(test_fn(x=a))
```

```
## [1] "a"
```

```r
# Expected : "a"

# Function
print(test_fn(x=mean))
```

```
## [1] "mean"
```

```r
# Expected : "mean"

# Constant
print(test_fn(x=1))
```

```
## [1] "1"
```

```r
# Expected : "1"
```
