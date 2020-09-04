---
title: "Programming Languages, Part A: Best MOOC Ever?"
date: 2020-09-04T17:52:22+02:00
Description: "Review of the Coursera MOOC Programming Languages (Part A)"
Tags: ["Course", "MOOC", "Review"]
Categories: ["Blog"]
DisableComments: false
---

I took so many MOOCs over the past three years (I lost count but they gotta
be around 30), but this one was _the hardest_ in terms of content, homeworks,
and quizzes... but also the most fun! It is actually
[the first part of a conceptually 3-part course](https://www.coursera.org/learn/programming-languages),
and I am not exaggerating in saying that this is the best MOOC I ever took,
because I thoroughly enjoyed every part of it, and I can't wait to take the
other parts.

The following is a relatively quick review of what this course is about (I
will use "the course" to refer to part A that I actually took and finished).
Each section is either one of the course's general goals or one of my own
observations about it.

# Language choice

The instructor Dan Grossman (who is a great teacher, by the way) made it very
clear that his language choices depend on the suitability of the language as
a vehicle for introducing the programming concepts he wants to teach, and
they are:

- **Standard ML** for part A
- **Racket** for part B
- **Ruby** for part C

From what I know about popular languages, I think SML would feel _really_
weird for anyone used to such languages, but not so much for those used to
functional languages. I say this because I tried a little bit of Haskell on
my own and found those two languages to be similar to each other than any
other language I tried, including R, Python, and JavaScript.

Here is an implementation of the popular functions `map()` and `filter()` in
SML:

```sml
fun map (f,xs) =
    case xs of
        []     => []
      | x::xs' => (f x)::map(f,xs');

fun filter (f,xs) =
    case xs of
        []     => []
      | x::xs' => if (f x)
                  then x::filter(f,xs')
                  else filter(f,xs');
```

# Functional programming

This course, and the next one, has a huge focus on concepts that belong to
functional programming (FP) or at least close to it. Things like recursion,
pattern matching, higher-order functions, and closures take up a huge part of
the course and associated homeworks. In between this big concepts, there are
small tips about performance, style, and other odds and ends that glue these
things together.

I find this paradigm very interesting because I come mainly from the R world,
which is a bit of a hybrid between functional and other paradigms that allow
mutation. When I learned Python, I found the concept of mutation (especially
methods that modify the object in place and return `None`) kind of annoying.
So, I already gravitate toward learning more FP.

# Not too theoretical; not too pragmatic

Most programming MOOCs and tutorials out there fall into two categories:

1. The theoretical kind, like an academic data structures & algorithms course
   in a computer science degree program. (I never took any of those.)

1. The practical, "let's build something" kind (which is obviously taking
   over the internet).

This course is surprisingly in the middle! It doesn't let you build something
practical like a small app or a game, but it also doesn't get too heavy with
theory and notation. I might say it has just the right amount of either side.

# Challenging & rewarding

This is literally stated at the welcome notes of the course, and I
wholeheartedly agree! The course material is dense and requires serious focus
to understand the concepts if they are new. There are 3 homework assignments.
Each contains roughly 10-15 coding problems to solve where the solution could
be a one-liner or as long as 15-20 lines. There is also a final exam which is
longer (and obviously harder) than your average Coursera "quiz".

In short, this course will get you to _think_, and if you are like me, you
will definitely enjoy that.

---

As someone with huge interest in learning programming, I found this course so
informative and fun, and I hope this review encourages other programmers to
take it. Of course, I am looking forward to starting the second part of the
course on Racket. (Oh, Lisp...)
