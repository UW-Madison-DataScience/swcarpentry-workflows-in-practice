# Collaboration: Using Version Control to Work with Others

**Based on material first developed by Lauren Michael**

## Overview

One of the best ways to collaborate on programs and other text-based files 
when collaborating with others is to use GitHub (or a group server) to host 
an "authoritative" repository that everyone can contribute to.

Let's say you've got a shared set of files in your research group that 
everyone will need to see and contribute to AND you'd like to use version 
control for this set of files. Instead of sending new updates of a project folder 
between eachother or using a department filesystem that doesn't have version control, 
you could use GitHub (or a group server) as the central location that each of you 
can pull from and push to using Git.

In this exercise, you'll each contribute to an authoritative repository 
within a GitHub *organization*. You'll first 'fork' a copy of the organization's 
repository in your own GitHub account and 'clone' a copy to your laptop, where 
you'll make changes. From then on, you'll always update your local laptop copy 
from the authoritative organization copy on GitHub. When you've made changes to 
your local copy, you'll first 'push' your changes to the repository in YOUR GitHub 
account, and then make a pull request from your GitHub repository to the 
organization's authoritative repository on GitHub. 

Importantly, this type of workflow can be used extensively with 
a range of collaborative research work, including code development, draft 
writing, developing laboratory protocols, etc. In all cases, git and GitHub 
will keep track of which version of each file existed at various times in 
history, and which changes were made. (GitHub organization repositories can also 
be accessed from off campus and by anyone that your group decides, which might be an 
advantage over using a more private group server or department filesystem.)

## Setting Up a Group GitHub Account

For this example, we'll use the UW-Madison-ACI organization account for the 
authoritative repository. While we won't go through the details of creating 
and managing an organization account in GitHub, your research group could 
create one on the following page: https://github.com/organizations/new

Public group repositories are FREE, but your group could opt for a a private, 
fee-based repository, instead. For public organizations, anyone 
with access to GitHub can view the contents of the repositories and make pull 
requests (just as for GitHub user accounts). With either type of repository (public 
or private), the 'owners' of an organization control who has the authoritiy to merge pull 
requests and otherwise directly affect repositories in the account.

More details about creating and managing organization repositories can be found 
in GitHub's help pages: 
https://help.github.com/articles/creating-a-new-organization-account/

## Exercise: Clone the Group Repository to Your Computer

First, let's navigate to our group repository in GitHub, in this case, the 
'swcarpentry-workflows-in-practice' in the UW-Madison-ACI account, 
here: https://github.com/UW-Madison-ACI/swcarpentry-workflows-in-practice

Click the green "Clone or download" button to the right, then copy the address 
of the repository in preparation for cloning it to your computer. Use the command 
line to navigate to your desired directory for the repository, then type

    $ git clone https://github.com/UW-Madison-ACI/swcarpentry-workflows-in-practice.git

You've now got a copy of the group repository on your laptop! You can check it 
by running the following commands:

    $ cd swcarpentry-workflows-in-practice.git
    $ ls
    $ git status

## More to Come


#### More than One Way to Clone

If the repository is served on an external (e.g., university)
server, you'll likely have to use git's ssh cloning
protocol. [Here](http://git-scm.com/book/en/Git-on-the-Server-The-Protocols#The-SSH-Protocol)'s
a great, short explanation of how to do that. GitHub's cloning protocol is
pretty simple, and described on the [Fork help
page](https://help.github.com/articles/fork-a-repo#step-2-clone-your-fork).

----
