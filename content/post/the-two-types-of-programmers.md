---
title: "The Two Types of Programmers"
date: 2020-08-08T20:00:56+02:00
Description: "Food for thought about programming styles and mindsets"
Tags: ["Coding"]
Categories: ["Blog"]
DisableComments: false
---

There is the programmer who thinks of code as means of getting something done,
and the other who actually cares about coding in and of itself. The former would
easily switch to a code-free tool if it is easier for the job. But the latter
gets obsessed with languages, syntax, style, efficiency -- things that are not
always directly related to solving a domain problem.

> _Which style is better?_

The answer is _it depends..._ (When is it not?) But here is some food for
thought about these programming approaches, mostly in the context of statistical
analysis and/or data science.

# Actually, it is a continuum

You might categorize these approaches in a binary fashion, but they are better
thought of as opposite extremes of a continuous scale. On one end lie the purely
get-it-done guys. On the other end, there are the coding nerds.  With that in
mind, you'd find out that most people lie somewhere in the middle and never at
the extremes.

## The practical extreme

Here are people who put the domain problem above all else. Don't worry too much
about code and just solve the problem. You can even ditch coding altogether and
use Excel or a GUI-based statistical package.

The keyword here is "practicality", and there isn't much else to say. If it
gives you the solution, it is good enough. You wouldn't want to waste time
worrying about whether or not you put spaces or how long your lines of code are.
You copied and pasted code multiple times? Fine. Wrote a `for` loop? Fine. Code
took a couple of minutes to run? Okay.

## The optimal extreme

Jumping right away to the other side, where code is the center of attention.
Writing `for` loops is a big no-no: use `purrr::map()` or `apply()`. Refactor
long pieces with clever tricks to make your code concise. A line must never
be more than 80 characters long, and always start a new line after `%>%`.
Needless to say, graphical interfaces are the evil banes of performance and
reproducibility. They are not even an option!

People argue against optimizing code, but no! Code must be efficient, reusable,
and readable. You don't want to come 5 days later and start deciphering
gibberish. Concise code is usually more readable. Elegant code is its own
reward! And the seconds (or even milliseconds) you save after optimizing the
code will add up if the code is rerun a lot.

# Why neither is right

Going all-in on one side means that you give up the advantages of the other.
If you focus on solving problems, that's perfectly fine. But you might find
bottlenecks in your process, like a slow piece of code or too much duplication.
On the other hand, the term "over-engineering" exists for a reason: focusing too
much on code speed or conciseness might waste time or make the code inaccessible
to others, because sometimes clever tricks are obscure.

# Moral of the story

Simply put, if you find yourself gravitating towards any of the two extremes,
try to pull yourself towards the middle. Strive to get the best of both worlds.
But sometimes, the current situation will need something specific. Tight
deadlines need getting things done, and massive data might force you into being
smart with code.

* * *

P.S. I often fall into the optimizing extreme. But at the day of writing this
post, I wrote a suboptimal regex in an exercise that solves the example string
but won't generalize to other cases. In an attempt to avoid over-engineering,
I tried to convince myself that passing the exercise is more than enough and I
should move on...
