---
title: "The Weird and Interesting Lisp Syntax"
date: 2020-09-27T12:05:48+02:00
Description: "Talking about the Lisp syntax and its advantages."
Tags: ["Coding"]
Categories: ["Blog"]
ffDisableComments: false
---

As I go through the course
[Programming Languages Part B](https://www.coursera.org/learn/programming-languages-part-b/),
which teaches programming concepts on the language Racket, let me reflect on
the strange syntax of Lisp (on which Racket is based).

![lisp-cycle](/post/lisp-syntax_files/lisp_cycles.png)

(Image source: https://xkcd.com/297/)

# Lisp? Racket?

I see that in a world full of Python and JavaScript, Racket and other Lisp
"dialects" are kind of obscure nowadays.
[Racket](https://en.wikipedia.org/wiki/Racket_(programming_language)) is a
(mainly) functional language, but I am here not to talk about its paradigm.

Racket's syntax is all about parentheses! Something like simple arithmetic
should be written like this in any common language:

```r
1 + 2 * 3 ^ 4
```

That would be actually written in Racket like this:

```racket
(+ 1 (* 2 (expt 3 4)))
```

This does what you'd expect from the first line of code, and as we learn in
any basic programming course, nesting works from the inside out: `expt` is
run first to give us 3 to the 4 which is then multiplied by 2 then added to
1.

That's too many parentheses already! But you should notice that the order of
symbols is different. This is because the arithmetic operators are _prefix_
functions which are called by putting them _inside_ parentheses:
`(function arg1 arg2 ...)` which is a bit different. Notice that this makes
parentheses an obligatory part of the syntax and not just to group things
together.

Let's take things up a level and see a piece of code that corresponds to a
variable definition and multi-branch if expression that uses that variable.

```racket
(define x 10)
(cond
  ((< x 10) "x is smaller than 10")
  ((> x 10) "x is greater than 10")
  (#t "x is exactly 10"))
```

Again, the parentheses nest everything. Even variable definitions are done
with functions inside parentheses. You can see the form `(cond (b1 e1) (b2
e2) ...)` in which `bi` is a boolean or an expression that evaluates to a
boolean, and `ei` is the expression that is run when a branch is true (all of
which are strings here).

Actually, just for better readability, any pair of parentheses can be
replaced by square brackets. This is commonly used to enclose `cond`
branches. So, we can rewrite the previous expression like this (I also added
whitespace to make it look like a table):

```racket
(cond
  [(< x 10) "x is smaller than 10"]
  [(> x 10) "x is greater than 10"]
  [#t       "x is exactly 10"])
```

As a final example, here is a function definition that uses `map` which takes
an anonymous function and a list of strings. The anonymous functions appends
a suffix at the end of each string.

**Note**: If you don't know about `map` and anonymous functions, check out
[my `map` tutorial](/post/funprog-map/) in which I explain these concepts and
their applications in R.

```racket
(define (string-append-map xs suffix)
  (map (lambda (x) (string-append x suffix)) xs))
```

# Why the syntax is interesting

Having parentheses for everything makes the syntax initially confusing. There
are no (infix) operators or any other forms of special syntax that make
pieces of code more or less distinguishable. But there is actually a couple
of benefits to that syntax.

## It is minimal

I am going to paraphrase the course instructor, Dan Grossman, here: the
syntax is so simple it can fit on one slide. Instead of having special syntax
for every construct (e.g. variable/function definitions, if/else statements,
function calls, etc.), Racket has most of its constructs as functions or
special forms that have almost identical syntax.

## It is unambiguous

In the arithmetic code written earlier, you need to remember how the
operations are ordered to code it correctly. A lot of syntax rules in
programming languages are like this. For example, the pipe operator in R
might not work the way you expect it when there are other operators before
it. (Try to work out which of e2 or e3 is equivalent to e1 in this piece of
code.)

```r
1 + 2 %>% exp()    # e1
1 + (2 %>% exp())  # e2
(1 + 2) %>% exp()  # e3
```

In Racket, however, the simple syntax leads to having only one way to do
things: every operator/function is prefix and you can nest them as deep as
you want because everything is already enclosed in parentheses.

---

Remember that opinions towards syntax are just opinions: they are subjective.
I do like that syntax and enjoy programming with it in the course. I am not
sure if I would ever get to use a Lisp dialect in a "real" application, but
that would be fun.
