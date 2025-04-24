# R basics

```{objectives}
- Knowing what types exist in R
- Knowing the most common data structures: vectors, lists, data frames, and sets
- Creating and using functions
- Knowing what a library is
- Knowing what `library()` does
- Being able to "read" an error
```


## Motivation for R

- **Free**
- Huge **ecosystem of examples, libraries, and tools**
- Relatively easy to read and understand
- Similar in scope and use cases to Python, Julia, and Matlab


## Basic types

```r
# integer
num_measurements <- 13L

# numeric (float)
some_fraction <- 0.25

# character (string)
name <- "Bruce Wayne"

# logical (bool)
value_is_missing <- FALSE
skip_verification <- TRUE

# we can print values
print(name)

# arithmetic operations with integers and numeric values
print(5 * num_measurements)
print(1.0 - some_fraction)
```

- R is **dynamically typed**:
  We do not have to define that an integer is an `integer`, we can use it directly,
  and R will infer it.
- Comments in R use the `#` symbol.


## Data structures for collections: vectors, lists, data frames, and sets

```r
# vectors (similar to Python lists, important for ordered elements)
scores <- c(13, 5, 2, 3, 4, 3)

# first element
print(scores[1])

# add items to vectors
scores <- c(scores, 4)

# sort vectors
scores <- sort(scores)
print(scores)

# lists are useful to store collections with named elements
experiment <- list(location = "Svalbard", date = "2021-03-23", num_measurements = 23)

print(experiment$date)

# add items to lists
experiment$instrument <- "a particular brand"
print(experiment)

if ("instrument" %in% names(experiment)) {
  print("yes, the list 'experiment' contains the element 'instrument'")
} else {
  print("no, it doesn't")
}
```
- **Vectors** are good when order matters and elements are homogeneous.
- **Lists** allow heterogeneous elements and are named collections.
- **Data frames** are like tables.
- **Sets** (`unique()` function or `sets` package) for collections without repetition.

You can nest:
- lists inside vectors
- vectors inside lists
- data frames inside lists
- lists inside data frames
- ...


## Iterating over collections

Iterating over a vector:
```r
scores <- c(13, 5, 2, 3, 4, 3)

for (score in scores) {
  print(score)
}

# example with string formatting
for (score in scores) {
  print(sprintf("the score is %s", score))
}
```

Iterating over a list:
```r
experiment <- list(location = "Svalbard", date = "2021-03-23", num_measurements = 23)

# iterating over values
for (value in experiment) {
  print(value)
}

# iterating over names and values
for (key in names(experiment)) {
  print(paste(key, experiment[[key]]))
}
```

## Functions

- Functions are like **reusable recipes**. They receive input arguments, perform operations, and return a result.
  ```r
  add <- function(a, b) {
    result <- a + b
    return(result)
  }
  ```

- Function summing elements in a vector:
  ```r
  add_all_elements <- function(sequence) {
    s <- 0.0
    for (element in sequence) {
      s <- s + element
    }
    return(s)
  }

  measurements <- c(1,2,3,4,5,6,7,8,9,10)
  print(add_all_elements(measurements))
  ```

- Function computing the mean:
  ```r
  arithmetic_mean <- function(sequence) {
    s <- add_all_elements(sequence)
    n <- length(sequence)
    return(s / n)
  }

  measurements <- c(1,2,3,4,5,6,7,8,9,10)
  mean <- arithmetic_mean(measurements)
  print(mean)
  ```

- Functions calling other functions and returning multiple values:
  ```r
  uppercase_and_lowercase <- function(text) {
    u <- toupper(text)
    l <- tolower(text)
    return(list(upper = u, lower = l))
  }

  some_text <- "SequenceOfCharacters"
  text_cases <- uppercase_and_lowercase(some_text)
  
  print(text_cases$upper)
  print(text_cases$lower)
  ```

**Why functions?** Reduce repetition and simplify understanding of the code.


## Reading error messages

Here we introduce a mistake and try to understand the traceback:

```{figure} img/r/error.png
:alt: Example error traceback
:width: 100%

Example error traceback. Can you explain the error?
```


## Libraries

Libraries are collections of functions. We load libraries to reuse functions defined in them.

Try this:
```r
library(stats)

measurements <- c(1,2,3,4,5,6,7,8,9,10)
result <- sd(measurements)
print(result)
```

Often, libraries are loaded directly:
```r
library(dplyr)
```

You can create your own libraries (packages) with functions for reuse.


## Great resources to learn more

- [R for Data Science](https://r4ds.hadley.nz/) (great for beginners)
- [The R Manuals](https://cran.r-project.org/manuals.html) (great for beginners)
- [Advanced R](https://adv-r.hadley.nz/) (intermediate level)


## Exercises

````{challenge} Exercise: create a function that computes the standard deviation
- Arithmetic mean:
  ```{math}
  \bar{x} = \frac{1}{N} \sum_{i=1}^N x_i
  ```
- Standard deviation:
  ```{math}
  \sqrt{ \frac{1}{N} \sum_{i=1}^N (x_i - \bar{x})^2 }
  ```
- Take this as starting point:
  ```r
  arithmetic_mean <- function(sequence) {
    mean(sequence)
  }

  standard_deviation <- function(sequence) {
    # your code here
  }
  ```
````

````{solution} Solution
```r
standard_deviation <- function(sequence) {
  mean <- arithmetic_mean(sequence)
  sqrt(mean((sequence - mean)^2))
}
```
````


````{challenge} Exercise: working with a named list
- Add more names and grades:
  ```r
  grades <- list(Alice = 80, Bob = 95)
  ```
- Print, modify, and explore the list.
````

````{solution} Solution
```r
grades$Craig <- 56
grades$Dave <- 28
grades$Eve <- 75
print(grades)

# Accessing a specific grade
print(grades$Eve)

# Names, values, and items
print(names(grades))
print(unlist(grades))
```
````


