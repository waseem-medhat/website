---
title: "Automating Git With Python"
date: 2020-09-16T10:53:36+02:00
Description: "Sharing a Python script that I wrote to update my website's Git repo."
Tags: ["Python", "Coding"]
Categories: ["Blog"]
DisableComments: false
---

Programmers are lazy! This is why I wrote a Python script to write one
command instead of three in my Git workflow.

# Context

This website is made with the static site generator
[Hugo](https://gohugo.io/). Once the layout and theme of the site are chosen,
all I needed then was writing new posts. This is done by writing Markdown
documents. I also have it version-controlled so that I can host it on
[Netlify](https://www.netlify.com/) through the GitHub repo.

So this is what happens with the repo after writing every new post:

- `git add .` (it's only one new file added to the repo)
- `git commit -m "my commit message"`
- `git push`

It is a repetitive task, and it is exactly the same except for the commit
message. Sounds like a perfect candidate for an automation script! (Also, a
fun Python exercise.)

# The code

Here's the whole script:

```python
#! /usr/bin/python3
from git import Repo, GitCommandError
import sys

if len(sys.argv) < 2:
    print("No message given... exiting")
    sys.exit()
else:
    commit_msg = sys.argv[1]

repo = Repo(".")
repo.git.add("--all")

try:
    repo.git.commit("-m", commit_msg)
    print(f"Successfully added commit: \"{commit_msg}\"")
except GitCommandError:
    print("Nothing to commit... exiting")
    sys.exit()

try:
    origin = repo.remote()
    origin.pull()
    print("Successfully pulled!")
    origin.push()
    print("Successfully pushed!")
except:
    print("Problem with pushing... exiting")
    sys.exit()
```

If you know a bit of Python and Git, you can very easily understand it. It
could have been more complicated to work in more use cases, but I did what
would help me with the exact repetition mentioned above.

The script is meant to be executed from the (Linux) shell, where I normally
run the Git commands, and takes the commit message as an argument:

```bash
./the_script.py "my commit message"
```

## Guards

I have put in some defensive code to avoid crashes or bad commits:

- Checking for the commit message argument so that the script exits if I
  forget to add the message to the execution command.
- Handling the exception that is raised when there is nothing to commit. This
  way the scripts prints a simple message instead of a Python traceback.
- Similar behavior with pushing.

## Assumptions

The script is far from perfect and, like I said, more can be done. But it
works for my specific use case:

- The repo and its remote are already set up.
- It commits all files (which is almost always one in my case).
- It doesn't care about branches (I commit to and push the master branch).

# Repos

I have this script, and
[a similar one written in R](/post/automating-git-with-r/) on GitHub:

- Python: https://github.com/waseem-medhat/git_done
- R: https://github.com/waseem-medhat/git_doneR

---

That's it! The idea is really simple but kinda cool. I am glad I was able to
write a script like this in an hour and have a Python workout in the process.
Now, I can update my website with one single command after writing this post
and the next ones!

**Edit**: I added a `git pull` command to the code. While my workflow so far has
the code only going in one direction, pulling is a best practice. Thanks to
David Kun for the suggestion.
