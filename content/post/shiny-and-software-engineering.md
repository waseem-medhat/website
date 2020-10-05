---
title: 'Shiny and Software Engineering'
date: 2020-10-05T20:26:32+02:00
Description: ''
Tags: ['R', 'Shiny', 'Coding']
Categories: ['Blog']
DisableComments: false
---

Why does Shiny code feel different from any other R code written for data
analysis or reporting?

I contemplated this question since I started learning Shiny, and here I will
talk about the idea that I have in mind to answer this question. The title
kind of gives it away, but it still deserves a more detailed explanation.

# My Shiny journey so far

At that time I started my Shiny journey, I already was comfortable writing R
code in both base and tidyverse "dialects". But then, Shiny felt like a
completely new thing. Building UIs was not hard because it is basically a
couple of nested functions, as if the R code mimics HTML (and it kind of does
because it generates divs and other elements eventually). However, I
struggled with making server logic for many reasons.

Even after being able to make code that works well, I still can't help but
feel there are better ways to write Shiny code. I know there are always more
tricks to discover no matter what kind of code I am writing. But this feeling
is always the strongest when I am making Shiny apps. So, why is that?

# We don't do software engineering

If I were to mention a single reason why Shiny is different or more
challenging, it is that Shiny is not just _programming_ in general, but also
has a lot of _software development_ or _engineering_ to it.

I couldn't put my finger on it at first, but when I heard it in an episode of
the [Shiny Developer Series](https://shinydevseries.com/) podcast, it made a
lot of sense to me.

{{< youtube kAYcIidygiU >}}

Yes, R programmers do have an idea about coding best practices. But the truth
is, for the most part, we don't have to follow them! Most analyses easily fit
in a single script. Even the script itself is usually nothing but a bunch of
top-level assignment statements and function calls, and if you slip in
repetitions, hard-coding or other code smells, you almost always can get away
with it.

On the other hand, based on my experience, Shiny gets very messy very
quickly. Try to put everything in a single `app.R` script and you will
easily find yourself drowning in hundreds of lines of code (assuming, of
course, you are not making a hello-world kind of app).

# What I do about it

Well, the canonical advice for any coding domain is to keep building stuff,
learn by doing, make mistakes and learn from them, etc. So I am currently
doing this, experimenting with different coding styles, and learning as I go.

For example, I started splitting the code into separate scripts and sourcing
those scripts into the main `app.R` one. So far, it works fine. But I have
just heard of Shiny modules which, if I understood its general idea
correctly, contains a UI/server part of an app that can be separated from the
rest of the code and can also be connected to other parts or integrated into
the main app somehow. It is one of the things I am looking forward to
learning currently.

---

The whole Shiny ecosystem is growing on me, and although I explained how it
is relatively challenging for a non-developer, I felt rewarded after
successfully building tools. I will sure document further steps in the
future.
