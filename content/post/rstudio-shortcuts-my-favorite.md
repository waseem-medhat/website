---
title: "RStudio Shortcuts (My Favorite)"
date: 2020-07-31T13:11:27+02:00
Description: "The most useful RStudio shortucts that I use on a daily basis."
Tags: ["R"]
Categories: ["Tutorials"]
DisableComments: false
---

RStudio has always been the most popular place for doing anything R-related:
scripts, Shiny apps, R Markdown documents, blogs, etc. It has a lot of features
that make R development more seamless. Among those, shortcuts are the most
helpful for statistics work because most of our work is not very complicated...

- On the scripting side, it's all about writing code and sending it to the
  console.
- On the (prose) writing side, text and R code is written in `.Rmd` files, which
  are then knitted.

I do care about workflow, and I think using shortcuts is the most fundamental
way of improving workflow. They help make coding faster and less painful
(physically, because my fingers hurt after too much typing). So, let me share
some of my favorite shortcuts. I have them laid out in a roughly categorized
manner and also summarized in a single table at the end.

# Find your workflow

Before I start dropping down the shortcuts I wanted to share, I should
re-emphasize that these are _my_ favorite shortcuts. RStudio has a lot of other
shortcuts that I won't mention (and others that aren't even bound to any keys).
You should explore the available shortcuts and pick the ones that suit you. This
brings us to the first shortcut:

- `Alt+Shift+k` to show a list of RStudio shortcuts.

# Operator shortcuts

The most important pair of shortcuts are those used to insert the assignment and
pipe operators. If you don't use them, _you should_. Not only do they help with
writing the operators, they also insert spaces around the operators, which is
good coding practice.

- Pipe operator (`%>%`) with `Ctrl+Shift+m`
- Assignment operator (`<-`) with `Alt+-`

![operator shortcuts](/post/rstudio-shortcuts-my-favorite_files/short_operator.gif)

# Jumping between panes

I am one of those people who believe that using the mouse in coding interrupts
their workflow. So, I try to minimize mouse usage as much as I can. One of the
ways I do so is by using RStudio shortcuts to switch focus to panes.

- Switch focus to the editor with `Ctrl+1`
- Switch focus to the console with `Ctrl+2`
- Switch focus to the help page with `Ctrl+3`
- Switch focus to the terminal with `Alt+Shift+t` (and start a terminal if there
  isn't one open already)

There are more focus shortcuts, but these are the one I use a lot.

# Jumping between tabs

While I am not a fan of opening lots of tabs, I usually do it in R projects
because I don't worry about where they lie. If I need a specific tab, I search
for it very quickly with a shortcut.

- `Ctrl+Shift+.` to search for an open tab.

![operator shortcuts](/post/rstudio-shortcuts-my-favorite_files/short_tabs.gif)

# Running code

Sending code to from the editor to the console is something any full-time R
programmer does hundreds of times a day. Imagine how much time (and pain) is
saved if you use a shortcut instead of selecting a number of lines with the
mouse and click the "Run" button time and time again. The shortcut is smart
enough to run the whole paragraph if it is a `dplyr` pipeline or `ggplot2`
paragraph.

- `Ctrl+Enter` runs current line or multi-line statement.

There is one extra trick, though. This shortcut runs the paragraph and moves the
cursor to the next line/paragraph. This might be slightly annoying if you are
tweaking a single parameter and re-running the code multiple times. RStudio has
a variant of the shortcut that doesn't move the cursor, but this shortcut is
unbound. So, you can go to the RStudio settings and bind it to whatever key
combination you like.

# Completion

RStudio's completion engine is really powerful, and I think it is one of the
best features of RStudio. It is already available for use out of the box, but I
tweaked some settings to make it even faster.

- Trigger completion after 2 characters instead of 3.
- Very tiny delay to make it trigger almost instantly.

![completion](/post/rstudio-shortcuts-my-favorite_files/completion.png)

Completion is also associated with its own keyboard shortcuts.

- `Ctrl+Space` to manually trigger completion.
- `Esc` to close an open completion window.
- `↑`/`↓` to navigate up/down in the completion choices.
- `Ctrl+p`/`Ctrl+n` can be used instead of `↑`/`↓`.

I personally like navigating with `Ctrl+p`/`Ctrl+n` because they are closer to
home row on the keyboard than the arrow keys.

# Commenting out lines

This a simple but handy shortcut. You can trigger comments on and off on a line
or a selection of lines. Very useful for debugging.

- `Ctrl+Shift+c` for triggering comments.

![operator shortcuts](/post/rstudio-shortcuts-my-favorite_files/short_comment.gif)

# R Markdown

Besides typing text and adding markup, probably the two most common tasks one
does with R Markdown are adding R code chunks and knitting the documents. Not
surprisingly, they have their own shortcuts.

- `Ctrl+Alt+i` to insert an R code chunk.
- `Ctrl+Shift+k` to knit R Markdown documents.

# Vim mode

This is not technically a shortcut or a set of shortcuts. It is a full editing
mode based on the very powerful text editor Vim. I won't give a Vim tutorial
here, but I will say this much: Vim is a game changer when it comes to editing
code. It has a rather strong barrier to entry because it works in a different
way than most modern applications, but after that barrier is a huge boost in
coding productivity and reduction in the distance between my thoughts and the
editing tasks I perform.

RStudio has a Vim-like editing mode which is good enough for basic Vim commands.
It lacks a lot of the real Vim magic, but what is already there is good most of
the time... It's an
[80-20 situation](https://en.wikipedia.org/wiki/Pareto_principle).

* * *

So, these are my favorite RStudio shortcuts. They really helped me with my R
workflow, and I hope they help you with yours, too.

TL;DR? Here is the full list.

| Key | Function |
|:---|:---|
| `Alt+Shift+k` | List all shortcuts |
| `Ctrl+Shift+m` | Insert pipe operator |
| `Alt+-` | Insert arrow/assignment operator |
| `Ctrl+1` | Switch focus to editor |
| `Ctrl+2` | Switch focus to console |
| `Ctrl+3` | Switch focus to help |
| `Alt+Shift+t` | Switch focus to terminal (start a new terminal if there is none) |
| `Ctrl+Shift+.` | Search for an open tab |
| `Ctrl+Enter` | Run current line or multi-line statement |
| _(Unbound)_ | Run current line or multi-line statement (keeping the cursor in place) |
| `Ctrl+space` | Trigger completion |
| `↑` or `Ctrl+p` (in completion) | Navigate up |
| `↓` or `Ctrl+n` (in completion) | Navigate down |
| `Ctrl+Shift+c` | Trigger comment |
| `Ctrl+Shift+k` | Knit R Markdown document |
