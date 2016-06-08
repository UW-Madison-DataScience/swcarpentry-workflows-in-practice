# Mobility: Using Version Control at Work and Laptop

**Based on material by Matt Gidden**

## Overview

One of the powerful ways to use version control is to maintain your development 
workflow as you move between different computers at work, 
at home, and anywhere else you might find yourself developing code.

Let's say you've been working on a project for a while on your laptop at home, and 
now you want to be able to continue developing the same files on a computer at work. 
Instead of sending new updates of the code to yourself via email each time, you 
can use an authoritative repository location, like GitHub, to quickly and easily 
update your laptop and work computer copies of the project, all while keeping a consistent 
history of your changes across all computers. Importantly, this type of workflow can be used extensively with 
both research work (i.e. developing code, writing drafts) and personal activites 
(i.e. updating a personal website), and across any number of computers.

## Exercise: Adding a Report to Our Python Development Directory

For this example, we'll add changes to our `planets` repository by 
specifically creating and editing a report file. We'll use 
three repository locations - a server, a work computer, 
and a home laptop computer. The "server" will host the authoritative
or 'base' repository and could be anywhere you have a connection to. For 
this example, we'll use GitHub as the server, but if you have access to 
a server on campus that is appropriate (e.g., server.wisc.edu), you could 
host your base repository there (and it's private!). 

To represent separate "Laptop" and "Work" computers, we'll say 
that your current copy of `planets` is your "Laptop" copy, and we'll use 
a separate "Work" directory to represent your work computer. After setting up 
a clean `planets` repository on GitHub, we'll then be able to push and 
pull changes between the "Work" and "Laptop" copies of the 
repository computers, keeping all repository copies up-to-date. Below are the 
major steps we need to take

### Set up the "Laptop" repository

Let's start by preparing our original copy of the project directory (our 
`planets` directory). Make sure to `cd` into the directory first.

Check the status of your repository:

    $ git status
    
Make sure that there are no more changes to commit and that the right files 
are ignored.

### Set up the "Server" repository

*In the workshop, we've already done this in a previous lesson, so we'll skip it!*

However, here's how you would do this for another repository in the future:
* Go to your page on the GitHub website (https://github.com/username), and click on your "Repositories" tab.
* Click the green "New" button toward the top right.
* Enter in the name of our repository's directory ("`planets`") and a description if you like, and then click the green "Create repository" button (without modifying any other options).

On the page that appears after creating the repository, you'll notice 
that one suggested next step is to "push an existing repository from 
the command line". In your `planets` directory on your laptop (the "Laptop" copy), do the following:

Check the remotes of your Laptop repository:

    $ git remote -v
    
Add the address of the GitHub repository as a remote named "origin" 
and then push our Laptop `planets` contents to the GiHub repository, 
just like the GitHub page says to:

    $ git remote add origin https://github.com/YOU/planets.git

### Update the "Server" repository

Before proceeding, make sure your "Server" repository is up-to-date 
with your most recent changes to `planets`.

    $ git push -u origin master
    
You should now be able to see that your repository files from the Laptop 
appear in your online GitHub repository for `planets`!

### Clone the repository to your "Work" computer, and do some work

Now we want to be able to work with the contents of our `planets` 
repository on a different computer. To represent this other computer, 
let's create a "Work" directory in the home directory.

    $ cd ~
    $ mkdir Work
    $ cd Work

Now we need to clone our planets repository from "GitHub" (our server) to 
the "Work" computer. Make sure to replace "YOU" or to grab the repository address 
from your `planets` repository page on GitHub.

    $ git clone https://github.com/YOU/planets.git
    $ ls
    planets

Let's `cd` into planets and look around at the files. Also, take a
gander at that remote.

    $ cd planets
    $ ls -a
    $ git remote -v

Now we can make some changes on the Work copy of the repository. Let's add a file, commit it 
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
First `cd` into the Laptop `planets` directory (not the one in "Work"), 
then:

    $ git pull origin master

Our Work and Laptop copies are synced! Check with an `ls` command to see that 
the `report.tex` file now exists in our Laptop copy of `planets`.


* * * * 
**Exercise On Your Own: Add details to the report file!**

Alright, now that you have the workflow down, use commands similar to the above 
to do the following:

1.  Add a statement to the `report.tex` file in your "Laptop" copy of the planets 
directory - something simple like "This is an 
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

#### More than One Way to Clone

If the repository is served on an external (e.g., university)
server, you'll likely have to use git's ssh cloning
protocol. [Here](http://git-scm.com/book/en/Git-on-the-Server-The-Protocols#The-SSH-Protocol)'s
a great, short explanation of how to do that. GitHub's cloning protocol is
pretty simple, and described on the [Fork help
page](https://help.github.com/articles/fork-a-repo#step-2-clone-your-fork).

----
