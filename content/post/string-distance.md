---
title: "Getting Started with String Distance Metrics"
date: 2020-08-15T18:08:18+02:00
Description: "My brief learning experience with string distance metrics and approximate matching"
Tags: ["R", "Text Analysis"]
Categories: ["Blog"]
DisableComments: false
---

I took a little digression from Python and NLTK when I discovered the R package
`stringdist`, which has a collection of functions for string distance
calculation and approximate matching based on those metrics. This is one of the
main reasons I started learning NLP in the first place, and `stringdist`, like a
lot of R packages, has good documentation including a [paper about the package
and underlying metrics](http://www.markvanderloo.eu/files/statistics/loo.pdf).
There was no better reason for me to start diving in right away!

So, here I am sharing some information that I learned.

# Context

If you are typing in a search box, the worst (working) implementation would
search for an _exact_ match of what you are typing: the tiniest typo would
totally blow your search query. But search implementations should be "smarter"
than that: accounting for some margin of error is essential whenever the user
input is free text. Part of the solution is attributed to _approximate_ (aka
fuzzy) string matching, and this is where a package like `stringdist` would come
in handy.

**Side note:** this is not really cutting edge. Algorithms in this package are a
level-up from exact matching, but are still simpler than machine learning models
that are used in actual search engines and might include other
features to improve search results.

# Types of distance metrics

According to the paper, there are 3 major types of algorithms for calculating
distance. I will glance over them in this section.

## Edit-based distance

Algorithms in this category calculate the distance between two strings based on
the number of edits of one string that are required to match another string.
These edits can be:

- insertions (`"fo" -> "for"`),
- deletions (`"care" -> "car"`),
- substitutions (`"fuzz" -> "buzz"`), or
- transpositions (`"pat" -> "apt"`).

The algorithms differ in whether they allow only one, some, or all of these
edits. For example, the longest common substring (LCS) method only allows
insertions and deletions. They also differ in the range of possible values.

```r
stringdist("foo",  "boo",   method = "lcs") # 2
```

## q-gram distance

In the context of such algorithms, q-gram is simply a string of length q. So, a
q-gram-based method takes its input strings and computes corresponding q-grams.
For example, given q = 2, `"fizz"` would produce 3 q-grams (`"fi"`, `"iz"`, and
`"zz"`). The calculations are then performed on these q-gram sets.

One q-gram-based method is the Jaccard method which calculates the proportion of
uncommon q-grams. You could guess that it ranges from 0 to 1.

```r
stringdist("leia", "leela", method = "jaccard", q = 2) # 0.8333
```

## Heuristic distance

Two methods were mentioned in the paper: the Jaro distance and its extension,
the Jaro-Winkler distance. These methods are actually developed to account for
typing errors using the logic that typing errors result in character
substitutions or transpositions between adjacent characters. The further the
matched characters are from each other, the larger the penalty added to the
distance metric.

They range from 0 to 1, where 0 is a perfect match.

```r
stringdist("comonality", "commonality", method = "jw") # 0.0303
```

# Application

The use of such methods is mainly a _lookup_ function: input string(s) is
searched into another set, the dictionary, for matches. A function like
`stringdist::amatch()` calculates the distance metric of interests and picks up
the best match. Also, it is straightforward to write a function that gets the
best n matches along with the calculated metric if you wish.

It is worth noting that different metrics produce different results, and such
difference might be huge. So, the choice should be consciously made based on the
type of text being analyzed. Also, since they don't have the same ranges of
possible values, they are not directly comparable.

* * *

That sums up what I have learned about string distance and approximate matching
from reading the `stringdist` package paper. From here I will probably get back
to progressing in Python and NLTK to continue learning.
