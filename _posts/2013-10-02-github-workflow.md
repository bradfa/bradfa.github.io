---
layout: post
title: Github Workflow
date: 2013-10-02
comments: false
---

Most people who use source control still seem to work on things by themselves,
both at companies and in little open source projects.  This is sad.

Some of the projects I work on for my job are just me coding and no one else.
I'm much worse at my job working like this than if I work directly with someone
else writing code and doing design.  I know this as in the past 2 years I've
worked both just by myself on software projects, with another engineer on a
firmware project, and I've sent patches upstream to u-boot.  Here's why:

When it's just me writing code, no one stops me from committing to master things
that are broken, half baked, or that have errors in them.  It's just me and my
flaws show through (I am flawed).  This is OK for little things or one-offs but
it's not a good idea for anything critical like a product or an open source
project that others will use.

When it's me and one or more other people all working on a code base, code
review can be really easy and simple.  For instance, in the office we
implemented a required code review process within Github using their pull
request feature.  No one is allowed to commit their own code to master or any
other branch in the company account for the project.  Each engineer forks the
main repo to their own account (don't worry, private repos are still private
when forked and the company still has full control over who can access them) and
then sends pull requests to the master on the main company repo.  Yes, this is
exactly what Github wants you to do!  This is awesome as you get code review for
free!  But even more importantly, you're less likely to ask someone to review
code that might be shit, so I found myself spending more time to make sure I did
things right and in ways that are maintainable.  This made a huge impact on our
bug counts for bugs present 24 hours or more after initial commit to master on
the company repo, we ended up having only 1 so far and that was due to the data
sheet making difficult to understand recommendations on how to step the core
voltage (no, I won't got into any more detail than that, sorry).

But the best type of software development process is many eyes and a crowd of
people who will have to maintain your code once you're gone, like u-boot or
Linux.  The maintainers know they will have to fix your bugs and that you
probably won't still be around when those bugs are found.  Hence, the
maintainers are going to be sticklers for making sure your code is clean,
readable, and maintainable before they accept it.  This is one step better than
the previous concept as the deadlines within any one company or organization
have no effect since the big group is spread across many companies and they want
only one thing: To make the codebase work in the long term.

Now, every time I'm working on something by myself I get annoyed.  I want that
other person / people to drive me to be better, to not let me cheat and commit
shit.  It's hard to impose on myself.  I think that's normal.
