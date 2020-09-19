---
title: "Hands on data.table"
date: 2020-09-18T18:04:23+02:00
Description: "A tutorial on the basic syntax of the R package data.table."
Tags: ["R"]
Categories: ["Tutorials"]
DisableComments: false
---

The `data.table` package introduces "enhanced" data frames, concise syntax, and
fast data processing, so let's learn about it!

I won't give any more introductions except that this tutorial is mostly based on
the package's introductory vignette, but I will include some of my own
observations and opinions as well. You could find the vignette
[here](https://cran.r-project.org/web/packages/data.table/vignettes/datatable-intro.html)
or you could load it (after installing the package) with this command:

```r
vignette("datatable-intro")
```

Let's get started!

# Creating `data.table`s

Before working on `data.table` objects, let's explore the methods we can use to
create one.

## Reading from a file/URL

The function `fread()` allows you to read from local files (e.g. CSV) or
external URLs.

```r
flights <- fread("flights14.csv")
```

## Building it manually

Creating a `data.table` here is almost identical to creating base R's data
frames, except that the function is named `data.table()` instead of
`data.frame()`.

```r
my_dt <- data.table(
  id = c("b", "b", "b", "a", "a", "c"),
  a  = 1:6,
  b  = 7:12,
  c  = 13:18
)

my_dt
#    id a  b  c
# 1:  b 1  7 13
# 2:  b 2  8 14
# 3:  b 3  9 15
# 4:  a 4 10 16
# 5:  a 5 11 17
# 6:  c 6 12 18
```

## Converting an existing data frame

The function `data.table()` mentioned earlier can be given a data frame to be
converted to a `data.table` object. It's that simple!

However, There is another function that is a little bit tricky because R usually
doesn't work that way. That function is `setDT()`.  The tricky part is that it
_modifies_ (or mutates) the existing object. It doesn't return a new object for
you to assign somewhere. It doesn't return anything! Because of that, you cannot
use `setDT()` on an built-in data frame (e.g. `iris`, `mtcars`) unless you
assign it into a variable in your environment.

```r
iris_df <- iris
setDT(iris_df) # same as `iris_df <- data.table(iris_df)`
```

# Subsetting `data.table`s

First of all, since a `data.table` are "enhanced" version of the conventional
data frame, basic functions that work on data frames still work on
`data.table`s. Also, string columns don't get automatically converted to factors
(which _was_ the default behavior in base R pre-version 4.0).

```r
class(my_dt)
# [1] "data.table" "data.frame"

summary(my_dt)
#       id                  a              b               c
#  Length:6           Min.   :1.00   Min.   : 7.00   Min.   :13.00
#  Class :character   1st Qu.:2.25   1st Qu.: 8.25   1st Qu.:14.25
#  Mode  :character   Median :3.50   Median : 9.50   Median :15.50
#                     Mean   :3.50   Mean   : 9.50   Mean   :15.50
#                     3rd Qu.:4.75   3rd Qu.:10.75   3rd Qu.:16.75
#                     Max.   :6.00   Max.   :12.00   Max.   :18.00
```

The square-bracket subsetting syntax `[]` is what encloses the special
`data.table` syntax. So, its basic premise is the same as base R. But
`data.table` adds a lot of features on that syntax.

## Subsetting rows

Subsetting rows with `data.table` is exactly the same as base R's subsetting,
except that _the comma is optional_ if no columns are chosen.

```r
my_dt[ c(1, 4, 6) ] # same as `my_dt[ c(1, 4, 6), ]`
#    id a  b  c
# 1:  b 1  7 13
# 2:  a 4 10 16
# 3:  c 6 12 18

my_dt[ id == "a" ]
#    id a  b  c
# 1:  a 4 10 16
# 2:  a 5 11 17
```

Although this indexing method is usually meant for subsetting, you could
actually use it to _order_ your table by some column. This is not special to
`data.table`, but it is kind of a neat trick.

```r
my_dt[ order(id) ]
#    id a  b  c
# 1:  a 4 10 16
# 2:  a 5 11 17
# 3:  b 1  7 13
# 4:  b 2  8 14
# 5:  b 3  9 15
# 6:  c 6 12 18
```

## Subsetting columns

Again, the syntax here is similar to base R. But there are additional points to
be considered.

- The variable names are used without quotation marks.

```r
my_dt[ , c ]
# [1] 13 14 15 16 17 18
```

- The default behavior of 1-column subsets is to be converted to a vector
  (instead of 1-column `data.table`) unless that variable is wrapped in
  `list()`.  Also, there is an alias for `list()` to be used in `data.table`
  syntax, and that alias is `.()` -- a dot instead of `list`.

```r
my_dt[ , .(a) ] # same as `my_dt[ , list(a) ]`
#    a
# 1: 1
# 2: 2
# 3: 3
# 4: 4
# 5: 5
# 6: 6
```

- The `.()`/`list()` syntax can be used to subset multiple columns.

```r
my_dt[ , .(a, c) ]
#    a  c
# 1: 1 13
# 2: 2 14
# 3: 3 15
# 4: 4 16
# 5: 5 17
# 6: 6 18
```

- Named lists can be used in `.()`/`list()` to rename columns.

```r
my_dt[ , .(col_a = a, col_c = c) ]
#    col_a col_c
# 1:     1    13
# 2:     2    14
# 3:     3    15
# 4:     4    16
# 5:     5    17
# 6:     6    18
```

Here is some additional column-subsetting syntax:

- The conventional base R way (with a character vector):
  - `my_dt[ , c("arr_delay", "dep_delay") ]`
- Selecting columns using column names stored in a variable with `..`:
  - `my_dt[ , ..variable_with_names ]`
- Deselecting columns with `!` or `-`:
  - `my_dt[ , !c("a", "c") ]`
  - `my_dt[ , !..variable_with_names ]`
  - `my_dt[ , -..variable_with_names ]`

# Aggregation

This is where things get more interesting. Within the same pair of brackets, you
could actually perform aggregation (summary statistics). Of course, this
operation can be combined with row-subsetting.

```r
my_dt[ , sum(a) ]
# [1] 21

my_dt[ , .(mean_a = mean(a), mean_b = mean(b)) ]
#    mean_a mean_b
# 1:    3.5    9.5

my_dt[ id == "b", .(mean_a = mean(a), mean_b = mean(b)) ]
#    mean_a mean_b
# 1:      2      8
```

There is a special symbol `.N` which gets the number of rows/sample size.

```r
my_dt[ a >= 3, .N ]
# [1] 4
```

Aggregation is most useful when it is grouped, and this is where we take
`data.table`'s syntax to an even higher level: there is a `by=` argument that we
can use also inside the square brackets. This argument takes a variable name or
multiple names with the same `.()`/`list()` syntax.

```r
my_dt[ , .N, by = .(id) ] # same as `my_dt[ , .N, id ]`
#    id N
# 1:  b 3
# 2:  a 2
# 3:  c 1
```

Instead of `by=` There is another argument named `keyby=` which actually sorts
the groups.

```r
my_dt[ , .N, keyby= id ]
#    id N
# 1:  a 2
# 2:  b 3
# 3:  c 1
```

# Chaining `data.table` operations

So far, we have been discussing operations that have matching "verbs" in `dplyr`
(e.g. `filter()`, `select()`, `summarize()`, `group_by()`). But there is another
important feature: chaining operations (for which `dplyr` uses the pipe operator
`%>%`). So can we chain operations in `data.table` code?

The answer is yes. Actually, it requires no additional syntax if you think about
the following logic: 

1. The operation starts with a `data.table` object followed by square-bracket
   syntax.

2. The output of that operation is also a `data.table` object, which (you
   might have noticed) is also the starting point of step 1!
   
After performing one operation on a `data.table`, a new operation can be added
_directly after the previous one_ with no need for intermediate variables or
even special operators like the pipe.

In the next example, I made the same operation from the previous example, which
had a column `N`. Then, I used that `N` column in a new subsetting operation.

```r
my_dt[ , .N, keyby = id ][ N > 1 ]
#    id N
# 1:  a 2
# 2:  b 3
```

# Other perks of `data.table`

So far, the whole tutorial has been about the syntax of making and working with
`data.table`s, now let me describe some othe features and advantages for using
the package:

- Operations are optimized for speed in both reading and manipulating data. This
  makes `data.table` quite popular among those who work with big datasets or
  care about the speed of their programs in general.

- When printing long tables, column names do not only print at the top, but also
  at the bottom. You will be spared a couple of mouse scrolls.

- There is a little detail that I find quite nice: if you call `fread()` trying
  to import a local file and it couldn't find the file, it raises the error but
  also prints the current working directory. I usually forget to check the
  working directory, so I find that quite helpful.

- If you haven't noticed, the syntax is quite concise. You could do so much in
  one line.

# My personal comments

I think `data.table` is quite an interesting package, and the next points sum up
my own opinions after getting started with the package along with some
comparisons to its popular counterpart `dplyr`.

- **Philosophy**: this package's syntax and style feel like an extension to base
  R's syntax. This is different from the `dplyr` which changes the style of R
  code into something that is more English-like and more verbose, which takes us
  to the next point...

- **Conciseness**: I honestly love concise code. It feels like a powerful thing
  to be able to semantically produce very much with as little code as possible,
  which is why `data.table` is quite interesting to me. Look at these two pieces
  of code for doing the same set of operations in both `data.table` syntax and
  `dplyr` syntax, assuming I start with a base R data frame and convert it to
  the corresponding package's object type before proceeding.

```r
# data.table
data.table(mtcars)[ am == 1, .(mmpg = mean(mpg)), by = cyl ][ order(mmpg) ]

# dplyr
tibble(mtcars) %>% filter(am == 1) %>% group_by(cyl) %>% summarize(mmpg = mean(mpg)) %>% arrange(mmpg)
```

- **User-friendliness**: this is where my opinion of `data.table` stops being so
  positive. The syntax and semantics are based on a rather sound understanding
  of how R works, especially lists. A moderately sophisticated piece of
  `data.table` syntax might look like gibberish to a beginner. On the other hand,
  the power of `dplyr` (and also is its main "selling" point) is how the syntax
  is, like I said earlier, very English-like in its writing and reading.

---

We're done playing with the basics of `data.table`! I hope you enjoyed it as
much as I did.
