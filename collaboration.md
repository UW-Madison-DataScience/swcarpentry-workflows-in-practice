# Collaboration: Using Version Control to Work with Others

**Based on material first developed by Lauren Michael**

## Overview

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
and managing a new organization account in GitHub, your research group could 
create one through the following page: https://github.com/organizations/new

Public group repositories are FREE, but your group could opt for a private, 
fee-based repository, instead. For public organizations, anyone 
with access to GitHub can view the contents of the repositories and make pull 
requests (just as for GitHub user accounts). With either type of repository (public 
or private), the 'owners' of an organization control who has the authority to merge pull 
requests and otherwise directly affect repositories in the account.

More details about creating and managing organization repositories can be found 
in GitHub's help pages: 
https://help.github.com/articles/creating-a-new-organization-account/

## Exercise: Fork the Repository from the Organization to Your GitHub Account

First, let's navigate to our group repository in GitHub, in this case, the
'swcarpentry-workflows-in-practice' in the UW-Madison-ACI account,
here: https://github.com/UW-Madison-ACI/swcarpentry-workflows-in-practice

Click the 'Fork' button in the top right. If GitHub wants you to choose 
which account to fork to, make sure to choose YOUR user account.

## Exercise: Clone the Repository from Your GitHub Account to Your Computer

Now, from the repository page in YOUR GitHub account, click the green "Clone 
or download" button to the right and copy the address 
of the repository in preparation for cloning it to your computer. Use the command 
line to navigate to your desired directory for the repository: (The "YOU" in 
the below address will be replaced withyour GitHub username.)

    $ git clone https://github.com/YOU/swcarpentry-workflows-in-practice.git

Now you've got a copy of the group repository on your laptop! You can check it 
by running the following commands:

    $ cd swcarpentry-workflows-in-practice.git
    $ ls
    $ git status

Also, YOUR GitHub copy of the repository has been automatically set 
as the "origin" remote for the local repository. Check it with:

    $ git remote -v

## Exercise: Add the Organization as the Upstream Remote

In order to make sure that you'll be able to pull future changes 
from the authoritative group repository, add it as another remote 
named "upstream" to represent the fact that it exists upstream from the "origin" 
copy you cloned from YOUR GitHub account.

    $ git remote add upstream https://github.com/UW-Madison-ACI/swcarpentry-workflows-in-practice.git
    $ git remote -v
 
## Exercise: Create a New File and Push to Your GitHub Account

Now, create a .txt file in your repository directory on your laptop, named 
according to your first initial and last name 
(like LMichael.txt) with three lines of inoccuous information about yourself, 
similar to the following:
    
    Lauren Michael
    I like blue skies.
    Horses are cool.

If you are uncomfortable having your name and details added to 
our public group repository, later, you can use a made-up name or celebrity 
you think others will not choose.

##### ON YOUR OWN
Commit the changes to your local repository, then push to YOUR GitHub repository. 
Check your repository on GitHub to confirm the changes are there.

## Exercise: Create a Pull Request to the Group Repository

When viewing your GitHub user copy of the `swcarpentry-workflows-in-practice` 
repository, click the "Pull requests" tab toward the top of the page. Then, 
click the green "New pull request" button to start a new pull request.

Make sure that the "base fork" is the "UW-Madison-ACI" repository 
while the "head fork" is your own copy on GitHub, then click the 
green "Create pull request" button.

Confirm the pull request comment, then click the next green "Create pull request" 
button. You should now see your pull request! If you'd like to see the pull requests 
of other workshop attendees as they're added, refresh the "Pull requests" tab page.

## Wait for the Workshop Instructors to Merge Your Pull Request

The instructors will merge your pull request after reviewing your changes, similar 
to how group members would for a research group repository.

## Exercise: Update your Local Copy from the Group Repository

Run the following commands within your local `swcarpentry-workflows-in-practice` 
directory to pull and view changes that were made to the group repository:

    $ git pull upstream master
    $ ls

You should now see everyone else's files, and have completed the basic workflow:
- Periodically pull from the authoritative group repository to update your working copy.
- Push new changes in your working copy to your repository on GitHub.
- Create a pull request to the group repository so someone can review and merge your updates.
- - Repeat
----
