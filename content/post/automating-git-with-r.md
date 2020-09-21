---
title: "Automating Git With R"
date: 2020-09-21T17:38:03+02:00
Description: "Sharing an R script that I wrote to update my website's Git repo."
Tags: ["R", "Coding"]
Categories: ["Blog"]
DisableComments: false
---

Just like the
[Python script I wrote earlier](/post/automating-git-with-python/),
I made a similar one in R to automate a simple sequence of Git commands. This
post will also be quite similar in structure to that other post with the Python
script.

# Context

This blog is made with [Hugo](https://gohugo.io/), and posts are written in
Markdown format. The whole site is basically a Git repository that gets pushed
to GitHub and is built and hosted on [Netlify](https://www.netlify.com/). After
writing every post, I write this series of Git commands:

- `git add .` (it's only one new file added to the repo)
- `git commit -m "my commit message"`
- `git push`

I automated these commands earlier using a Python script that can be executed
from the command line like this:

```bash
./the_script.py "my commit message"
```

Now, I will show the code that does a simple functionality in R.

# The code

```r
#! /usr/bin/Rscript

library("gert")

args = commandArgs(trailingOnly = TRUE)

if (length(args) == 0) {
  cat("No message given... exiting\n")
  q("no")
}

if (nrow(git_status()) == 0) {
  cat("Nothing to commit... exiting\n")
  q("no")
} else {
  git_add(".")
  git_commit(args[1])
  cat(paste("Successfully added", args[1], "\n"))
}

git_pull()
cat("Successfully pulled!\n")
git_push()
cat("Successfully pushed!\n")
```

The logic is almost identical, and you could work it out without having solid
understanding of both languages. Although, if you examine the Python script, you
will find that I didn't put any pull/push guards. This is because R's errors
don't take up more than one line and are informative on their own, unlike
Python's bulky tracebacks. (Or I'm rationalizing being lazy!)

The extra caveat in R is that (at least in Unix-like systems) the command `R` is
not the one to use to run scripts from the command line. It's `Rscript`, which
you should see in the "shebang" line at the top of the script.

## Assumptions

Just like the Python script, this one works on a couple of assumptions that
might make it a bit less useful for other programmers:

- The repo and its remote are already set up.
- It commits all files (which is almost always one in my case).
- It doesn't care about branches (I commit to and push the master branch).

# Repos

You can already see that the code is not too big, and I already pasted it here
for reading convenience. I do have it on GitHub, though:

- R: https://github.com/waseem-medhat/git_doneR
- Python: https://github.com/waseem-medhat/git_done

---

That sums up my quick exercise of automating Git in R and making it an
executable script to run from the command line.
