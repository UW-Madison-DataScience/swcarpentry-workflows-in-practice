[Up To Schedule](../../../README.md#schedule) - Back To [Make Changes from Anywhere (GitHub)](../github/Readme.md) - Forward To [Collaborate](../collaborate/Readme.md)

# Mobility: Using Version Control at Work and Home

**Based on material by Matt Gidden**

## Overview

One of the powerful ways to use version control is to maintain your workflow
between different computers at work, at home, and anywhere else you might find
yourself doing "work". This type of workflow can be used extensively with both 
research work (i.e. developing code, writing drafts) and personal activites 
(i.e. updating a personal website).

The workflow in this section describes three repository locations - a server, a
work computer, and a home computer. The "server" will host the authoritative
or 'base' repository and could be anywhere you have a connection to. For
example, you could use your GitHub repository as the server. If
you have access to a server on campus that is appropriate (e.g., server.uni.edu), 
you can host your base repository there (and it's private!).

For the purposes of this exercise, we'll use GitHub to store the authoritative
'base' repository, and we'll use different directories on your laptop to represent
two different computers you might do work on ("Laptop" and "Work"). For example, 
we'll use ~/work to represent your work computer, and pretend like ~/work is 
effectively the home directory (or other location) on your work computer.

## Exercise: Adding a Report to Python Development Directory

Let's say you've been working on your stats module for a while on your Laptop, and 
now you want to be able to continue developing the module on your Work computer. 
Instead of sending new updates of the code to yourself via email each time, you 
can use an authoritative repository location, like GitHub, to quickly and easily 
update your Laptop and Work copies of the project, all while keeping a consistent 
history of your changes across all computers.

### Set up the "Laptop" repository

Let's start by preparing our Laptop copy of the project directory (our 
`simplestats` directory). Make sure to `cd` into the directory first, 
then ...

Check the status of your repository, to make sure that only our `stats.py` and `test_stats.py` files are tracked.

    $ git status
    
Make sure to ignore the `data` directory, so that we're not going to track its contents for our GitHub and Work respositories. Remember the `.gitignore` file and to check the status of the repository when done.

### Set up the "Server" repository

Now let's go to GitHub to initiate and empty repository that we can push to:
* Go to your page on the GitHub website (https://github.com/username), and click on your "Repositories" tab.
* Click the green "New" button toward the top right.
* Enter in our the name of our repository's directory (`simplestats`) and a description if you like, and then click the green "Create repository" button.

On the page that appears after creating the repository, you'll notice 
that one suggested next step is to "push an existing repository from 
the command line. So let's do it!

In your `simplestats` directory on the Laptop, do the following:

Check the remotes of your Laptop repository (we shouldn't have any yet):

    $ git remote -v
    
Add the address of the GitHub repository as a remote named "origin", just like the GitHub page says to:

    $ git remote add origin https://github.com/YOU/simplestats.git
    
Check the remotes list again to confirm success, and then push your repository contents to the GitHub remote, just like the GitHub page says to:

    $ git push -u origin master
    
You should now be able to see that your repository files from the Laptop 
appear in your GitHub repository for `simplestats`!

### Clone the repository to your "Work" computer, and do some work

Now we want to be able to work with the contents of our `simplestats` 
repository on a different computer. To represent this other computer, 
let's create a "Work" directory in your home directory.

    $ cd ~
    $ mkdir Work

Now clone our simplestats repository from "GitHub" (our server) to the "Work" 
computer.

    $ git clone https://github.com/YOU/simplestats.git
    $ ls
    simplestats

Let's `cd` into simplestats and look around at the files. Also, take a
gander at that remote.

    $ cd simplestats
    $ ls -a
    .  ..  .git  README.md  stats.py  test_stats.py
    $ git remote -v
    origin  https://github.com/YOU/simplestats.git (fetch)
    origin  https://github.com/YOU/simplestats.git (push)

Now we can make some changes on the Work computer. Let's add a file, commit it 
to the repository, and push our changes back to the GitHub repository (our 
"origin" remote):

    $ touch report.tex
    $ git add report.tex
    $ git commit -m "added the base tex file for my report"
    $ git push origin master

### Update the "Laptop" repository, and do some more work

Let's say we're working on our Laptop computer again, and now we want to add 
details to our report file, so we need to update our Laptop repository. 
First `cd` into the Laptop `simplestats` directory (not the one in "Work"), 
then:

    $ git pull origin master

Our Work and Laptop copies are synced! Check with an `ls` command to see that 
the `report.tex` file now exists in our Laptop copy of `simplestats`.

#### Aside: Version-Control Best Practices

At this point, you're fully set up to work in a best-practice, version-control
work flow. Experience shows that it's best to work in branches (i.e., other than
master) to make sure the master branch stays up-to-date with your server's
(origin's) master branch. This stuff may not be intuitive when you're first
starting out, though, so just play around and get used to the general work flow
for now. You'll get better at it over time.

#### Aside: Latex and the Limits of the Version Control Workflow

Have you ever struggled with formatting Word's equations, chapters,
bibliography, etc.? [Latex](http://www.latex-project.org/) works wonders with
that. Here's a great graph taken from Marko Pinteric's
[website](http://www.pinteric.com/miktex.html) that explains the difference.

![wordvlatex](https://raw.github.com/gidden/boot-camps/mobility/version-control/git/mobility/wordvslatex.gif "Word vs. Latex")

With the advent of Google Drive, it's often as easy to use that tool if a
document is simple enough, i.e., on the left side of the curve (where Word is
easier than Latex). Note that Google Docs is version controlled as well.

Furthermore, simply **imagine** having to write something as complicated as a
prelim or thesis using Word. You'd spend as much time formatting the thing as
you do actually writing the content. In other words, it's worth the (smallish)
headache of getting used to Latex in order to use it for bigger
documents. There's even a [Wisconsin Thesis
Template](https://github.com/willb/wi-thesis-template)! That's right, you'd have
to do **0** work to correctly format your thesis. 

Finally, and this is pure aesthetics, Latex looks **good**. Have you ever read a
paper and thought "wow, those equations look great"? It's likely written in
Latex. Plus, once you write your first paper, you have all the infrastructure to
write the next one. You can literally copy the files into a different directory
and rewrite content. Super simple.

Latex works great with the workflow described here because it's text-based. You
are literally altering text files, so there's **nothing else** going on behind
the scenes. Word files, etc., have lot's going on under the hood, and so are
poor candidates for version control. 

#### Aside: Setting Up a "Base" Repository

If you want to use GitHub as your repository host, you can safely skip this. If
you want to use a university server as your repository host, you'll have to go
through these steps.

We'll start off in the home directory and create a bare repository in a new
directory.

    $ mkdir server
    $ cd ~/server
    $ git init --bare myrepo.git

You'll see a new directory in ~/server named myrepo.git. If you ```cd``` into
myrepo.git and give an ```ls``` command, you'll see the contents of the .git
directory you saw earlier in the [Use Version Control](../local/Readme.md)
section.

    $ cd myrepo.git
    $ ls
    branches  config  description  HEAD  hooks  info  objects  refs

This is git's way of storing your repository's information. You shouldn't touch
this, and you can safely ignore it.

#### Aside: Bare Repositories

A bare repository is meant to simply **store** your files. It actually stores
the contents of the .git directory that you see in all normal repositories. It's
generally not meant to be touched by a human's hands, and is designed to
communicate through git with other non-bare repositories. In fact, when you
initialize a new repository on GitHub, GitHub's version is a bare repository.

Why use a bare repository? The answer is that non-bare repositories don't always
play nice together, and it turns out it helps to have a single, base repository
that's "always right". You can get a more detailed answer
[here](http://www.gitguys.com/topics/shared-repositories-should-be-bare-repositories/).

#### More than One Way to Clone

If the repository is served on an external (e.g., university)
server, you'll likely have to use git's ssh cloning
protocol. [Here](http://git-scm.com/book/en/Git-on-the-Server-The-Protocols#The-SSH-Protocol)'s
a great, short explanation of how to do that. GitHub's cloning protocol is
pretty simple, and described on the [Fork help
page](https://help.github.com/articles/fork-a-repo#step-2-clone-your-fork).

----

[Up To Schedule](../../../README.md#schedule) - Back To [Make Changes from Anywhere (GitHub)](../github/Readme.md) - Forward To [Collaborate](../collaborate/Readme.md)
