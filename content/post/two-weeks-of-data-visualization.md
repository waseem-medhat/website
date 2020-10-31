---
title: "Two Weeks of Data Visualization"
date: 2020-10-31T20:40:50+02:00
Description: "Sharing my first two weeks revisiting data visualization"
Tags: ["Data Visualization"]
Categories: ["Blog"]
DisableComments: false
---

In this post, I document my first two weeks diving back into data visualization
while working with the web-based tools D3.js and React, from silly SVG faces to
interactive scatter plots.

# Learning Material

First of all, I would like to say that most of my work was done through learning
from the open course "Datavis 2020" by Curran Kelleher.

# Output

All visualization folks like to say "a picture is worth a thousand words." So, I
will share this picture that sums up my two weeks' worth of work.

![vizhub summary](/post/two-weeks-of-data-visualization_files/)

Now, I will try to explain my progress in more detail.

## Silly SVG Face

![silly svg face](/post/two-weeks-of-data-visualization_files/)

That is probably the silliest thing you could do while learning "data
visualization", except that its purpose was learning how to work with SVG. D3
(or probably all web-based data vis) is supposed to render SVG shapes. So,
before working with actual data, it was a good idea to practice building shapes
with SVG and making sure it is drawn with variables and very little math to make
it pixel-perfect.

## Basic Plots

![basic plot](/post/two-weeks-of-data-visualization_files/)

While this visually seems like a direct next step, much has been going on
between that SVG face and this. There is a combination of React, D3, and vanilla
JavaScript that I had to learn in order to build a bare bones bar chart or
scatter plot.

- **D3** has wide functionality like helper functions for data fetching, data
  manipulation, scales to convert the data range to pixel

