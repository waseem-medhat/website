---
title: 'Data Visualization as a Slide Deck'
date: 2020-11-06T00:10:38+02:00
Description: 'Presenting a data visualization project in the form of a slide deck.'
Tags: ['Data Visualization']
Categories: ['Projects']
DisableComments: false
---

This project is an example of multiple data visualizations telling a story
together in the form of a slide deck. These visualizations are originally
made by Cole Nussbaumer Knaflic (see [this video](https://youtu.be/X79o46W5plI)),
and my effort lies in reproducing that presentation in a web-based form to
practice (and demonstrate) my skills with these technologies.

# Final presentation

Here is an animated GIF showing all the slides.

![vis_slides](/post/data-visualization-as-a-slide-deck_files/vis_slides.gif)

# Sequence

First of all, the power of presenting data visualizations in multiple slides
lies in its sequential nature. It enforces the storytelling aspect of your
vis. Instead of presenting a single chart and using it to explain everything,
you can create a sequence of copies with slight modifications. Then, you tell
the story once piece at a time.

# Using color to shift focus

![color focus](/post/data-visualization-as-a-slide-deck_files/color_focus.png)

One of the most important differences between slides is the use of color to
emphasize pieces of visualization and tune others out. So that each slide
focuses on a different part of the story.  If the current slide is mentioning
some information about products C, D, and E, then the "accent" blue color should
be given to the lines of those products while other elements take the gray color
to make them less demanding of the viewer's attention.

# Explanatory annotations

![explanatory annotations](/post/data-visualization-as-a-slide-deck_files/explanatory_annotations.png)

I want to emphasize the distinction between _explanatory_ and _exploratory_
visualizations. Explanatory means that the visualization communicates a
specific finding or recommendation, which is reached after analyzing the data
beforehand. On the other hand, exploratory visualizations are not tied to
specific information. They only present the data, and whoever sees the
visualization is the one that tries to find insights and draw conclusions. To
put it shortly, _exploratory visualizations are tools for analysis, and
explanatory visualizations are tools for communication_.

In explanatory visualizations, annotations are usually a good idea to
emphasize the insights presented by the charts. Also, they can be used with
color to effectively replace a color legend.

# Technologies

This is a web-based project, so it relies heavily on JavaScript.

- [D3.js](https://d3js.org/) does data-related tasks like importing,
  manipulation, and scaling the data values as pixel values to be used by the
  rendered elements.
- [React](reactjs.org/) renders and organizes UI elements.
- [MDX Deck](https://mdx-deck.jxnblk.com/) renders React components as a
  web-based slide deck using Markdown syntax.
