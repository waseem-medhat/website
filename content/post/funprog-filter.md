---
title: "Functional Programming: filter"
date: 2020-09-14T19:01:12+02:00
Description: "A description of reduce as a functional programming concept, plus an R tutorial on using it"
Tags: ["R", "Functional Programming"]
Categories: ["Tutorials"]
DisableComments: false
---

Another famous higher-order function is `filter`. Although it is rather handy
for some programming languages, it might be less useful in the R world. I
will talk about it for the sake of completeness (I wrote two posts about
higher-order functions: [one about map](/post/funprog-map/) and
[another about reduce](/post/funprog-reduce/)). Then I will explain why we
don't need it in R

# What is `filter`?

Like the other higher-order functions we talked about, `filter` takes a
function and a collection. The result is a subset of the original collection.
Elements are kept or discarded, not surprisingly, according to the input
function:

- The input function takes an element of the collection and produces a
  boolean/logical, which is called a _predicate_.
- For each element of the collection, the predicate is called. If the
  predicate returns `TRUE` the element is kept, and if it returns `FALSE`
  (you guessed it) the element is discarded.

# How to implement it in R?

If you already know [map](/post/funprog-map/) and
[reduce](/post/funprog-reduce/), `filter` should be very easy. It is
available in base R with a capital F: `Filter()`.

Let's say you have a vector `c(1,2,3,4,5)` and you want to filter only even
numbers. The only trick you need to do is build a predicate, which we'll call
`is_even()`.

```r
is_even <- function(x) {
    x %% 2 == 0
}
```

All what's left is calling `Reduce()` with the predicate and the vector.

```r
Filter(is_even, 1:5)
# [1] 2 4
```

## Side note: negating a predicate

Although you could easily negate a logical vector with the exclamation/bang
sign, that doesn't make sense for a predicate: you can't negate a function.
But R has a built-in function called `Negate()` that takes a predicate and
return another predicate with the logic flipped. (Notice that this is a
higher-order function that is different from the ones we discussed because it
_returns_ a function, the new predicate.)

# Why is it not very useful?

One word: _vectorization_.

In case you don't know what that means, it is the fact that when you do an
arithmetic or logical operation on a vector. R automatically does it
element-wise. This is not the default behavior of most programming languages
in which it doesn't make sense to add a number to a collection. But R is a
language "made by statisticians for statisticians", and making vectorization
a default behavior is (I think) a smart move for a language meant to be used
by non-developers.

So, when I ask if the remainder of dividing "the vector" by two is zero, I
get back a vector of `TRUE`s and `FALSE`s.

```r
1:5 %% 2 == 0
# [1] FALSE  TRUE FALSE  TRUE FALSE
```

Which brings us to the second smart move: any vector can be indexed with
logical vectors, so that values matching the `TRUE`s are kept and those
matching the `FALSE`s are discarded.

Here is another example in which I will write both methods without any
intermediate definitions, and it's up to you to decide which is better to
your taste.

```r
Filter(function(x) x %% 1 == 0, iris$Sepal.Length)
#  [1] 5 5 5 5 5 5 5 5 7 5 6 6 6 6 5 6 6

iris$Sepal.Length[iris$Sepal.Length %% 1 == 0]
#  [1] 5 5 5 5 5 5 5 5 7 5 6 6 6 6 5 6 6
```

Personally, I feel slightly annoyed by the need to repeat the vector's name
to use the indexing-based method. But I also know that these higher-order
functions are kind of obscure in the R world.

Let's also not forget that R is meant for data analysis, and `Filter()`
doesn't work with data frames unless you convert them to a list. But why do
that when you have indexing-based filtering? or `dplyr`?

---

That ends our glance over the higher-order `filter` and, more importantly,
why R programmers don't need it.
