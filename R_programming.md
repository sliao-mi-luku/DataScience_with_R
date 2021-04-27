# R Programming

### Data structures

**rep**

```r
c(rep(5, times = 3), rep(6, times = 4)
```

**seq**

```r
seq(1, 10, by = 2)  # returns c(1, 3, 5, 7, 9)

seq(1, 5, by = 1)  # returns c(1, 2, 3, 4, 5)
```

**vector**

Create a default vector

```r
vector(mode = 'numeric', length = 5)  # returns c(0, 0, 0, 0, 0)
```

**matrix multiplication**

```r
arr1 = array(c(1,2,3,4), dim = c(2,2))
arr2 = array(c(-1,-2,-3,-4), dim = c(2,2))
res = arr1 %*% arr2
```

**adding columns/rows**

```r
x = c(1,2,3,4,5)
y = c(6,7,8,9,10)

z = cbind(x, y)
w = rbind(x, y)
```

**subset**

```r
subset(iris, Species == 'virginica' & Petal.Length > 5)
```

**allowing replacing data**

```r
attach(iris, warn.conflicts = FALSE)
```
