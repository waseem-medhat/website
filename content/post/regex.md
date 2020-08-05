---
title: "Gotta Love/Hate Regex"
date: 2020-08-05T01:46:25+02:00
Description: "Talking about regex in general and explaining an example"
Tags: ["Text Analysis"]
Categories: ["Personal"]
DisableComments: false
---

I remember once calling regular expressions "absolute magic". I do think it is
powerful, but it kind of gets messy and unreadable when it gets bigger. In fact,
one of those was the reason I wrote this post. It was in the NLTK book I am
currently reading, and it was a little more complex than what I usually use in
my code. So, here I am rambling about regex and trying to explain the one I
studied today as an example.

# The goal

That regex was supposed to to be used as a sort of word tokenizer on this
example string:

```
"'When I'M a Duchess,' she said to herself, (not in a very hopeful tone
though), 'I won't have any pepper in my kitchen AT ALL. Soup does very well
without--Maybe it's always pepper that makes people hot-tempered,'..."
```

There is more to words than being a set of alphanumeric characters separated by
whitespace. There is punctuation in the middle: hyphens, parentheses, full
stops, etc., but not every punctuation symbol actually separates two words.
You can see compound words (e.g. "hot-tempered") and punctuation without
whitespace like the double-hyphen.

# The solution

```
"\w+(?:[-']\w+)*|'|[-.(]+|\S\w*"
```

I never wrote a regex this long before. So, looking at it, my brain's first
response was "gobbledygook!" To be fair, though, this is relatively simple in
the grand scheme of things: they can get _really_ big.
([See for yourself...](https://stackoverflow.com/questions/201323/how-to-validate-an-email-address-using-a-regular-expression#201378))

# Breaking it down

Just like any programming problem, this one is better solved by breaking it
down. I will split it by the `|` because it means "or", so the whole regex
represent multiple choices, and we are trying to match _any_ of them.

## Part 1: `\w+(?:[-']\w+)*`

- The first part is `\w+` which searches for a word (i.e. one or more
  alphanumeric characters and/or underscores).
- The pattern `(?:___)` is for grouping a smaller regex. But what is the smaller
  regex's job, and why is it grouped?
- The smaller regex is `[-']\w+` which matches a hyphen or an apostrophe, and
  either is followed by a word. 
- The grouping is because this whole wrapped regex is followed by a `*` which
  means zero or more occurrences.

So this part can be thought of as the main pattern. It covers most of the
desired tokens including compound words that are separated with a hyphen (e.g.
"hot-tempered") as well as those with apostrophes (e.g. "I'M").

## Part 2: `'`

The string of interest had quotes written between literal single quotes. So, we
needed our pattern to cover those by, well... using a single quote.

## Part 3: `[-.(]+`

- The square brackets `[]` with a set of characters inside of it means that _any_
  of those characters should be matched.
- Here it is followed by a `+` to indicate that one or more of those characters
  should be matched.

This part captures punctuation marks like parentheses, full stops, ellipses, and
the double hyphen.

## Part 4: `\S\w*`

The last part cleans up with some final touches. It searches for a
non-whitespace character followed by 0 or more alphanumeric characters. Here it
picks up two tokens that wouldn't be split otherwise: a comma and a closing
parenthesis.

* * *

That's it! Although it is not the most complicated thing in the world, I still
it proves the point I said at the beginning: regex can be messy but still really
powerful!
