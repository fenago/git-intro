<img align="right" src="./logo-small.png">

# Lab:  Undoing Changes
One of the main advantages when using a version control system is the ability to undo changes and return to a previous version. Git provides powerful approaches and control over managing your repository and it's history which we'll explore in this scenario.


#### Tutorial Overview

In this scenario the environment has been created with a Git repository with a number of simple commits.
Let's get started.

#### Pre-reqs:
- Google Chrome (Recommended)

#### Lab Environment
There is no requirement for any setup.

There should be terminal opened already. You can also open New terminal by Clicking `File` > `New` > `Terminal` from the top menu.

Run the following command in **terminal**:
`cd ~/work/git-intro/4/ && mv git .git`

**Note:** To copy and paste: use **Control-C** and to paste inside of a terminal, use **Control-V**

You can access lab at `<host-ip>:<port>/lab/workspaces/lab4`

### Step 1 - Git Checkout
When working with Git, a common scenario is to undo changes in your working directory. The command git checkout will replace everything in the working directory to the last committed version.

If you want to replace all files then use a dot (.) to indicate the current directory, otherwise a list the directories/files separated by spaces.

**Task**

Use git checkout to clear any changes in the working directory.

**Solution**

`git checkout .`


### Step 2 - Git Reset
If you're in the middle of a commit and have added files to the staging area but then changed your mind then you'll need to use the git reset command. git reset will move files back from the staging area to the working directory. If you want to reset all files then use a . to indicate current directory, otherwise list the files separated by spaces.

This is very useful when trying to keep your commits small and focused as you can move files back out of the staging area if you've added too many.

**Task**

Move the changes from staging back to the working directory using git reset

**Solution**

`git reset HEAD .`

### Step 3 - Git Reset Hard
A git reset --hard will combine both git reset and git checkout in a single command. The result will be the files removed from the staging area and the working directory is taken back to the state of the last commit.

**Task**

Remove the changes from both the staging area and working directory using git reset

**Protip**

Using HEAD will clear the state back to the last commit, using `git reset --hard <commit-hash>` allows you to go back to any commit state. Remember, HEAD is an alias for the last commit-hash of the branch.

**Solution**

`git reset --hard HEAD`

### Step 4 - Git Revert
If you have already committed files but realised you made a mistake then the command git revert allows you to undo the commits. The command will create a new commit which has the inverse affect of the commit being reverted.

If you haven't pushed your changes then git reset HEAD~1 has the same affect and will remove the last commit.

**Task**

Use *git revert* to revert the changes in the last commit.

Note, this will open an Vim editor session to create a commit message for each commit. To save the commit message and quit vim type the command `:wq` for each Vim session.

**Protip**

The motivation behind creating new commits is that re-writing history in Git is an anti-pattern. If you have pushed your commits then you should create new commits to undo the changes as other people might have made commits in the meantime.

**Solution**

`git revert HEAD --no-edit`

### Step 5 - Git Revert
To revert multiple commits at once we use the character `~` to mean minus. For example, `HEAD~2` is two commits from the head. This can be combined with the characters ... to say between two commits.

**Task**

Use the command  **git revert HEAD...HEAD~2** to revert the commits between **HEAD** and **HEAD~2**.

**Protip**

You can use the command `git log --oneline` for a quick overview of the commit history.

**Solution**

`git revert HEAD...HEAD~2 --no-edit`


