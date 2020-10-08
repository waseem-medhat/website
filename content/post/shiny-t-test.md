---
title: 'Shiny t-Test App'
date: 2020-10-03T16:46:23+02:00
Description: 'Showcasing a shiny app that does the t family of tests.'
Tags: ['R', 'Shiny', 'Statistics']
Categories: ['Projects']
DisableComments: false
---

This is an R/Shiny app that performs the t family of tests (on data uploaded
by the user) with options that allow more flexible analysis.

Doing a t-test in R is really easy, but making an intuitive UI interface to
same test is more challenging than it seems. If you build apps with too many
assumptions in mind, the user might not share these assumptions, and that
would lead to bugs. I try to keep this in mind while making Shiny apps.

In this project demo, I will explain this app I built for t-tests in some
detail to demonstrate its features and flexibility as well as areas of
improvement that I intend to work on in my Shiny journey.

The app took more than one iteration. You can check out the latest version
both as GitHub code and live demo from the links below:

- App (shinyapps.io): https://waseem-medhat.shinyapps.io/shiny-t-test/
- Code (GitHub): https://github.com/waseem-medhat/shiny-t-test

# Iteration 1

![shiny t-test](/post/shiny-t-test_files/shiny-t-test.gif)

## Feature overview

The following points are the features and ideas I took into consideration
while making the app:

- The user uploads his/her own CSV data for analysis.
- Data (of interest for the test) could be long or wide
  - Parts of the UI which are responsible for variable selection should
    adapt to that fact.
  - An explanation of what long and wide formats are should be provided to
    users in a helper tool.
  - In the case of long data, a warning message will be displayed to the user
    if the chosen independent/grouping variable is not binary.
- There are checkboxes that directly correspond to the `paired=` and
  `var.equal=` arguments of the `t.test()` function.
- The analysis does not start as a direct reaction of changing the parameters,
  but after pressing a "Start" button.
  - The button is shown only when the user has set all parameters to prevent starting the test without specifying variable names.
- The output of the analysis includes simple descriptive analysis of each
  sample followed by the output of the test itself.

## Purpose

The ultimate purpose of this app is nothing more than my own Shiny training.
I simply wanted to build a functional app, and I consider this a first step
towards more complex projects that might actually solve a more "tangible"
problem.

However, I might argue that a long-vs-wide data feature is an interesting one
because it is usually not available in GUI-based statistical packages like
SPSS. When you perform a t-test (or any test in general), the program usually
expect one of the two forms. I know that in SPSS, the independent t-test
expects long data and the paired t-test expects wide data.

## Potential improvements

- **Expanded EDA section**: no test should ever be jumped to without a decent amount
  of exploration, more than seeing a histogram and the mean.
- **Assumption-checking**: again, no test should ever be done without
  checking assumptions. Tests of normality (e.g. KS, Shapiro) or equal
  variances (e.g. Levene) could be added.
- **The UI**: I know how to work with the UI beyond this simple and common
  sidebar layout. I could use more Bootstrap features or throw a theme on
  top. But my goal here was making something functional, not pretty.

# Iteration 2

This one builds further upon the previously written code. It addresses some
of the points mentioned earlier and adds some more.

![better shiny t-test](/post/shiny-t-test_files/better-shiny-t-test.gif)

## Added features

- Customizing the UI was the main focus of this version.
  - I used the tabbed layout provided by the `shinydashboard` package coupled
    with a dark theme from the `dashboardthemes` package.
  - UI elements are visually separated by boxes.
  - Warning alerts UI is improved.
- Added support for SPSS data files.
- The table is displayed after uploading and reading it to serve as a visual
  confirmation that the data have been read properly.
- Exploratory plots are customizable by the user to toggle the dashed mean
  line or the density curve.

## Potential improvements

- **Assumption-checking**: this is one of the points I mentioned about
  iteration 1 but didn't address.
- **Improving the code**: I am still experimenting with coding style when it
  comes to separating it into scripts and writing functions. Also, I am
  looking forward to using Shiny modules, so I might refactor the app to use
  them.
