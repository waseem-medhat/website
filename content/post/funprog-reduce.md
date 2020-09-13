---
title: "Functional Programming: reduce"
date: 2020-09-13T17:19:20+02:00
Description: "A description of reduce as a functional programming concept, plus an R tutorial on using it"
Tags: ["R", "Functional Programming"]
Categories: ["Tutorials"]
DisableComments: false
---

Continuing the theme of functional programming and
[higher-order functions](https://en.wikipedia.org/wiki/Higher-order_function#R),
this one is about another example: `reduce`. In my
[previous post](/post/funprog-map/index.html), I wrote about `map` and its use
generally in functional programming and specifically in R. This tutorial will
follow a similar structure.

![map](/post/funprog-reduce_files/reduce.png)

(Image source: https://iamit.in/blog/Higher-order-functions-in-Python-sorted-map-reduce-filter/)

# What is `reduce`?

`reduce` is quite an interesting function. It is sometimes known in other
languages as `fold`. Like `map` it takes as input a function and a collection
(e.g. list). Because this is _functional_ programming, the magic lies in the
input function. So, let me describe its behavior and how `reduce` uses it:

- The function takes two argument. The first is an _accumulator_ (we'll call
  it `acc`), and the second would correspond to an element in the collection
  (we'll call it `x`).
- `reduce` applies that function on each element of the collection in a way
  that the result of the first call (on the first element) is used as the
  _accumulator for the second call_, which returns another value to be used
  as the _accumulator for the third call_, and so on... In other words, with
  each element in the collection, the accumulator gets updated until a final
  value is obtained.

Unlike `map`, I believe it is hard to grasp from an abstract point of view
without examples, so I will get to that right away.

# How to implement it in R?

Let's start with a simple example. But before starting, I need to point out
that the function's name is `Reduce()` with a capital R.

If I want to sum a numeric vector `c(1,2,3,4,5)` with an algorithm that uses
`Reduce`, the logic is that the accumulator starts at 0, gets added to the
first element and 1 becomes the new accumulator. Then, it gets added to the
second element and 3 becomes the new accumulator, and so on... So, the
function that should be given to `Reduce()` takes an accumulator and a (new)
element and adds them. You can define that as an anonymous function.

```r
function(acc, x) {
    acc + x
}
```

After nailing down the function, we can now call `Reduce()` with the
anonymous function and the vector as arguments.

```r
Reduce(function(acc, x) {acc + x}, c(1,2,3,4))
# [1] 10
```

You can think that `reduce` performs the task like this:
`(((1 + 2) + 3) + 4)`

**Side tip**: you could actually use the plus sign wrapped in backticks \`+\`
which means you are using this
[infix operator](https://en.wikipedia.org/wiki/Infix_notation) as a function
to be passed (e.g. as an argument to `Reduce()`).

# Practical example

The previous example was a little bit silly, although you have to get silly
sometimes to introduce new concepts based on what you already know and are
comfortable with. The next example is a bit more practical. Our goal here is
merge two data frames by inserting one data frame _at a specific index_ (i.e.
in the middle) of another data frame.

Consider these example data frames:

```r
d <- data.frame(A = 1:4, B = c("AA", "BB", "DD", "EE"))
to_insert <- data.frame(A = 2.5, B = "CC")

d$ID <- seq(nrow(d))
to_insert$ID <- 2.5

d
#   A  B ID
# 1 1 AA  1
# 2 2 BB  2
# 3 3 DD  3
# 4 4 EE  4

to_insert
#     A  B  ID
# 1 2.5 CC 2.5
```

What I want to do is basically insert the data frame `to_insert` between row
2 and row 3 of the data frame `d`. There are two main things that need to be
done to get a `Reduce()` algorithm ready.

## Make a list out of the data frame

`Reduce()` need a collection to iterate (and accumulate) over. In this case, we need to build a "collection of rows". This is easily done with the function `split()`.

```r
d_split <- split(d, d$ID)
d_split
# $`1`
#   A  B ID
# 1 1 AA  1
#
# $`2`
#   A  B ID
# 2 2 BB  2
#
# $`3`
#   A  B ID
# 3 3 DD  3
#
# $`4`
#   A  B ID
# 4 4 EE  4
#
```

That takes care of one argument.

## Build the accumulating function

The accumulation in the previous example was done by addition. But in this
example, accumulation is actually row-binding. So, the accumulator will be a
data frame, and I will keep adding the rows of the list to that accumulator
_until I've reached the index of interest_, in which case I will also _bind
the data frame I want to insert_ before continuing the accumulation process.

```r
fn <- function(acc, row) {

  if (row$ID == 2) {
    rbind(acc, row, to_insert)
  } else {
    rbind(acc, row)
  }

}
```

## Putting it together

The final step is merely calling `Reduce()` with the pieces we built.

```r
Reduce(fn, d_split)
#      A  B  ID
# 1  1.0 AA 1.0
# 2  2.0 BB 2.0
# 11 2.5 CC 2.5
# 3  3.0 DD 3.0
# 4  4.0 EE 4.0
```

From there, you could easily work your way forward by abstracting this
algorithm into a function, or maybe adjust the row names.

---

That's it for `reduce`! Another interesting functional programming concept,
and R already has it built in.

P.S. The last example was inspired from
[a LinkedIn post by Adrian Olszewski](https://www.linkedin.com/posts/adrianolszewski_rockyourr-statistics-datascience-activity-6709076931184259072-_A5y)
in which he used a similar implementation but with `do.call()` instead of
`Reduce()`.
