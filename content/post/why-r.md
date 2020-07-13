---
title: "Why R (Biostatistician's version)"
date: 2020-07-13T22:56:09+02:00
Description: "This post describes why R is a good tool for biostatistics"
Tags: ["R"]
Categories: ["Tutorials"]
DisableComments: false
---

Contrary to the majority of R content which is directed towards data science and
related _business_ domains, this post is in the context of _biostatistics_.  So,
if you are a biostatistician (working or aspiring) let me explain why I think R
is a good investment of your time. I don't assume you have any prior knowledge
about programming, so I will provide some information about it in broad strokes.

![rstudio-windows](/post/why-r_files/rstudio-windows.png)

# Versatile

Most biostatisicians I know in academia use some combination of SPSS, MedCalc,
PASS, and/or Excel for their work. Arguably, all these tools can be replaced
with R and its packages which form an ecosystem that integrates multiple tools
for all purposes related to a statistician's work. There are also multiple
document writing packages which can help you even replace Word and PowerPoint
with R's environment.

For more advanced applications, R can interact with databases or scrape web
pages for data collection. Its modeling capabilities can be extended to machine
learning algorithms and neural networks. There is even a
[package](https://shiny.rstudio.com/gallery/) you could use to make web
applications that can interactively present any model or process made in the
backend with R.

# Educational

Using R (versus graphical statistical software) does not inherently give you
more education on statistics and modeling. But programming shifts your mindset
away from the end-user perspective and closer to the "creator" one, and the
latter is usually more concerned with how and why things work they way the do.
While both types of software contain documentation and references to the
book/paper on which a procedure is based, I've seen far more programmers mention
official documentation than graphical software users who might mostly rely on
tutorials and community posts, which could be more error prone than the original
resources. Again, let me re-emphasize that the relationship here is associative,
not causal. R is still a tool, and it will not _teach_ you anything.

Apart from the mindset and documentation, you could use simulation to _generate_
data and test any statistical theory or concept. I highly recommend it as a
powerful learning tool. One example I did before was simulating F statistics
from simple linear regression of generated data given some sample size and
correlation coefficient. The goal was to see the F value's sensitivity to these
two factors.

![](/post/why-r_files/sim.jpg)

# Plain text

Writing code in R or any other language is nothing more than writing plain text,
which means code can be easily copied, pasted, or manipulated by a text editor.
The code files are very small in size, so back-ups and transfers are also easy.
Another huge advantage is that they can be managed with version control systems
like git which tracks changes to the code, allows uploading to GitHub and
similar sites, and facilitates collaboration on coding projects.

The following line of code is a concise command that tells R to fit a linear
model using `height` as the dependent variable and `weight` as the independent
variable, and these variables are pulled from a dataset named `women`.

```r
lm(height ~ weight, data = women)
```

# Reproducible

This is a very important strength of programming, and it is underutilized in
many domains of medical research due to the lack of education and settling for
the "user-friendly" options. With graphical applications, you do your analysis
by clicking a series of buttons and/or menu options. If you are to share the
results, you have to either repeat the process in a live setting or send the
final data file with written explanation of the methodology that led to that
file.

With programming, _your methodology is your code!_ In other words, since
procedures in R are done by writing commands, this makes your project file much
closer to being self-explanatory. You could even add comments on the code to
clarify certain things if you want.

# Free

R is part of the increasingly popular
[free](https://en.wikipedia.org/wiki/Free_software) and open source software
(FOSS, or FLOSS where the L stands for libre), which is not just about providing
software that is "free of charge" but also respects the "freedom" of users and
encourages public, collaborative development. The opposite to that is the
proprietary software model in which some person or company controls the source
code, and no one else is able to obtain it unless it is made public by the
proprietor(s).

# Supported

A rather unique strength of R is that it is surrounded by a big and active
community that are passionate about it and helpful to each other and to
newcomers as well.  R-related questions and answers can be easily found on
[Stack Overflow](https://stackoverflow.com/questions/tagged/r?tab=Frequent), so
most (if not all) of your errors in your first learning steps have already been
addressed there. The R community on Twitter and LinkedIn also exchange lots of
Q&A and tips.

* * *

This is my own perspective of why R is such a great tool for biostatisticians to
learn and use. I hope you found it informative, and let me end it with a quote:

> "Programs like SPSS are busses, easy to use for the standard things, but very
> frustrating if you want to do something that is not already preprogrammed.  R
> is a 4-wheel drive SUV (though environmentally friendly) with a bike on the
> back, a kayak on top, good walking and running shoes in the passenger seat,
> and mountain climbing and spelunking gear in the back.  R can take you
> anywhere you want to go if you take time to learn how to use the equipment,
> but that is going to take longer than learning where the bus stops are in
> SPSS."
>
> --- <cite>Greg Snow</cite>
