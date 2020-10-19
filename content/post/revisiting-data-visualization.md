---
title: 'Revisiting Data Visualization'
date: 2020-10-19T01:49:26+02:00
Description: 'My past and future efforts with data visualization'
Tags: ['Data Visualization']
Categories: ['Blog']
DisableComments: false
---

Data visualization is one of the most interesting data science subdomains for
me, and now I decided to revisit my previous progress and build more on top
of it.

Actually, I invested a considerable time and effort into data viz. I read
books, participated in a couple of Makeover Monday challenges, and even had a
[visualization blog](https://vizplasty.wordpress.com/). So, in this post, I
will discuss a bit of my past data viz experiments including projects, tools,
and books.

# Projects

These are directly taken from my [old blog](https://vizplasty.wordpress.com/).
Head there if you want to look at more detailed descriptions of the projects
and my thought process.

## Aging America

This one was my first submission for the Makeover Monday challenge. I managed
to pull off a customized design to give it a more "infographic" look. One of
the most notable ideas are using text color to replace the typical color
legends and that lollipop chart in which the points visually form a line.

![aging america](/post/revisiting-data-visualization_files/aging_america.png)

## Cost of a night out around the world

This is more of a fancy-looking Tableau dashboard with interactive
functionality. It was another Makeover Monday challenge submission.

![cost of a night out](/post/revisiting-data-visualization_files/nightout.png)

## Sleep requirement pie chart

I reworked an already built visualization for this project. The original one
here was a pie chart. Aside from the fact that pie charts are generally
despised, this particular one was meaningless and unsuitable for the data to
be presented.

![pie chart before](/post/revisiting-data-visualization_files/pie_before.webp)

I made it into a visualization that has better aesthetics and is more
representative of the data. Not to mention it is customized to be a bit
different from the typical chart.

This is actually one of my favorite projects. I was really satisfied with the
output.

![pie chart after](/post/revisiting-data-visualization_files/pie_after.webp)

# Tools

Now that we are done with the colorful part, let's talk about the
technicalities. I tried a good number of the major visualization tools, and
here are my thoughts about them...

## R

Being a statistician who works with R, I did plots in R more than any other
tool. R has a ton of visualization functionality that I will put into three
categories: base R, `ggplot2`, and web-based graphics.

- **base R**: there is a built-in graphics package that low-level with _very_
  concise syntax. It is pretty powerful, but like most low-level coding, it
  kinda gets messy if you take it too far.
- **`ggplot2`**: is now the standard go-to package for making graphics in R.
  It a little more high-level than the base graphics package and has a more
  precise "grammar" of making plots and adding layers on top of them. Its
  power is even more realized with the tons of extension packages that
  open roads to so much stuff built on top of `ggplot2`.
- **web-based graphics**: the most common, and the only one I dealt with, is
  `plotly`. It is commonly used in `shiny` apps and has one particularly cool
  feature which converts any `ggplot2`-based plot into a web-based plot with
  just a single function.

No matter the package, R feels like a good middle ground between high-level
and low-level. It is code-based and highly extensible, but it doesn't force
you to work with every shape.

## Tableau

There is that one time in which I actually left coding and worked with the
GUI-based Tableau... What was I thinking?

The first couple of minutes on Tableau make you absolutely amazed! Drag
something from here, drop it there, and boom! You got yourself a plot. You
can also find a lot of cool stuff people make with Tableau. It is also packed
with a lot of sophisticated functionality.

After that, I started making dashboards and got tons of inconsistencies. Some
plots would not align well together. Others looked good in their own view but
actually looked ugly in a dashboard because everything gets smaller except
the text which maintains its size and now looks huge compared to the tiny bar
below it. My frustration with these things was way stronger than my will to
keep fighting the app or learn to do it in a "smarter" way. Because I believe
that the smarter way to do this is with _code_.

## D3

The JavaScript library D3.js works at a lower level than any visualization
tool I ever worked with. I learned it about two years ago, but forgot most of
what I learned because I didn't practice. While I was learning it, I was able
to make presentable projects like the sleep requirement pie chart rework.
D3's real power lies in its flexibility and interactivity. Here is a
[link to one of my favorite D3 works](https://www.visualcinnamon.com/portfolio/royal-constellations)
made by Nadieh Bremer. I know the design is fundamentally tool-agnostic, but
I usually associate D3 with visualizations that look like art.

For data scientists, though, D3 can have a huge barrier of entry. Before
getting started with D3, you need to pick up the fundamental web
technologies: HTML, CSS, and JavaScript. Also, I noticed that "real-life" D3
work is done with a front-end framework (mostly React).

# My future plan

On the theoretical side, I want to re-read some of the popular books that I
have already read once, especially Tufte's "The Visual Display of
Quantitative Information" and Knaflic's "Storytelling with Data". I might
also read new books.

On the practical side, I want to re-learn D3. All these awesome
visualizations made with this tool makes it too attractive for me to leave
behind. So, it will be my main tool for practice.

---

I hope the next visualization journey will be fun!
