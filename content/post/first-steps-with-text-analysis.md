---
title: "First Steps With Text Analysis"
date: 2020-07-18T14:30:56+02:00
Description: "Describing my the beginning of my journy in text analysis and NLP"
Tags: ["R", "Text Analysis"]
Categories: ["Personal"]
DisableComments: false
---

This is the beginning of a phase of experimenting with a new topic: text
analysis! I have always heard about text analysis or natural language processing
(NLP) for quite some time, but I never learned anything about it. So, it is
about time I got started...

# First resource

Since I mostly code in R, it was a natural choice to use it as a platform for my
learning. The book
["Text Mining with R: A Tidy Approach"](https://www.tidytextmining.com/) seemed
like a good choice for a starting point.

![](https://www.tidytextmining.com/images/cover.png)

At the time of writing this post, I have completed 4 chapters that introduced
the following topics:

- **The tidy text format** which follows the famous "tidy" table format by
  having one row per word (or token).
- **Tokenization** of text documents, i.e., splitting them into tokens. Tokens
  are either single words (unigrams) or pieces with more than one words
  (n-grams).
- **Sentiment analysis** by labelling tokens as positive/negative and analyzing
  them.
- Analyzing frequency and **tf-idf** as a measure of token importance in a
  document.
- **Network/graph** visualization to explore relationships between words.
