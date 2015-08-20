# Mobility: Using Version Control at Work and Home

**Based on material by Matt Gidden**

## Overview

One of the powerful ways to use version control is to maintain your development 
workflow when you need mobility as you move between different computers at work, 
at home, and anywhere else you might find yourself doing "work".

Let's say you've been working on a project for a while on your laptop, and 
now you want to be able to continue developing the same files on a computer at work. 
Instead of sending new updates of the code to yourself via email each time, you 
can use an authoritative repository location, like GitHub, to quickly and easily 
update your laptop and work copies of the project, all while keeping a consistent 
history of your changes across all computers. Importantly, this type of workflow can be used extensively with 
both research work (i.e. developing code, writing drafts) and personal activites 
(i.e. updating a personal website), and across any number of computers.

## Exercise: Adding a Report to Your Python Development Directory

For this example, we'll add changes to our `simplestats` repository by 
specifically creating and editing a report file. We'll use 
three repository locations - a server, a work computer, 
and a laptop computer. The "server" will host the authoritative
or 'base' repository and could be anywhere you have a connection to. For 
example, you could use GitHub as the server, which is what we'll use for 
the example. If you have access to a server on campus that is appropriate 
(e.g., server.uni.edu), you could host your base repository there (and it's 
private!). 

To represent separate "Laptop" and "Work" computers, we'll say 
that your current copy of `simplestats` is on your "Laptop", and we'll use 
a separate "Work" directory to represent your work computer. After setting up 
a clean `simplestats` repository on GitHub, you'll then be able to push and 
pull changes as you transition between working on the Laptop and Home copies 
of the repository. Below are the major steps we need to take

### Set up the "Laptop" repository

Let's start by preparing our Laptop copy of the project directory (our 
`simplestats` directory). Make sure to `cd` into the directory first, 
then ...

Check the status of your repository, to make sure that only our 
`stats.py` and `test_stats.py` files are tracked.

    $ git status
    
Make sure that there are no more changes to commit and that the files ending 
in `.pyc` are added to a `.gitignore` file.

### Set up the "Server" repository

Now let's go to GitHub to initiate an empty repository to serve as our base:
* Go to your page on the GitHub website (https://github.com/username), and click on your "Repositories" tab.
* Click the green "New" button toward the top right.
* Enter in our the name of our repository's directory (`simplestats`) and a description if you like, and then click the green "Create repository" button (without modifying any other options).

On the page that appears after creating the repository, you'll notice 
that one suggested next step is to "push an existing repository from 
the command line. So let's do it!

In your `simplestats` directory on the Laptop, do the following:

Check the remotes of your Laptop repository (we shouldn't have any yet):

    $ git remote -v
    
Add the address of the GitHub repository as a remote named "origin" 
and then push our Laptop `simplestats` contents to the GiHub repository, 
just like the GitHub page says to:

    $ git remote add origin https://github.com/YOU/simplestats.git
    $ git push -u origin master
    
You should now be able to see that your repository files from the Laptop 
appear in your online GitHub repository for `simplestats`!

### Clone the repository to your "Work" computer, and do some work

Now we want to be able to work with the contents of our `simplestats` 
repository on a different computer. To represent this other computer, 
let's create a "Work" directory in your home directory.

    $ cd ~
    $ mkdir Work
    $ cd Work

Now clone our simplestats repository from "GitHub" (our server) to the "Work" 
computer (make sure to replace "you" or to grab the address from the 
`simplestats` repository page on GitHub.

    $ git clone https://github.com/YOU/simplestats.git
    $ ls
    simplestats

Let's `cd` into simplestats and look around at the files. Also, take a
gander at that remote.

    $ cd simplestats
    $ ls -a
    .  ..  .git  stats.py  test_stats.py
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
    
You should now also be able to see the addition of this file on GitHub!

### Update the "Laptop" repository, in preparation for more work

Let's say we're working on our Laptop computer again, and now we want to add 
details to our report file, so we need to update our Laptop repository. 
First `cd` into the Laptop `simplestats` directory (not the one in "Work"), 
then:

    $ git pull origin master

Our Work and Laptop copies are synced! Check with an `ls` command to see that 
the `report.tex` file now exists in our Laptop copy of `simplestats`. Now you can


* * * * 
**Exercise On Your Own: Add details to the report file!**

Alright, now that you have the workflow down, use commands similar to the above 
to do the following:

1.  Add a statement to the `report.tex` file - something simple like "This is an 
awesome report" will be just fine for our example. Make sure to add and commit 
your change.

2.  Push the changes to your GitHub repository.

3.  Pull the changes down to the repository in your hypothetical "Work" computer, 
and check to see that your report.tex file has the added text!

* * * * 

#### Note: Version-Control Best Practices

At this point, you're fully set up to work in a best-practice, version-control
workflow. This stuff may not be intuitive when you're first
starting out, though, so just play around and get used to the general workflow
for now. You'll get better at it over time. When you'd like to extend this 
example to one of your own projects and/or use a group server instead of GitHub, 
you might also take a gander at the tips below.

## Tips for Your Own REAL Work

#### Latex and the Limits of the Version Control Workflow

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

#### Setting Up a "Base" Repository

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

#### Bare Repositories

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
