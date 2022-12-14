<img align="right" src="./logo-small.png">

# Lab: Committing Changes

in this lab, you'll learn how to view changes in your working directory and commit them to your repository. This environment has a Git repository with a committed file. In the working directory a change to the committed file exists and a uncommitted file.


Let's get started.

#### Pre-reqs:
- Google Chrome (Recommended)

#### Lab Environment
There is no requirement for any setup.

There should be terminal opened already. You can also open New terminal by Clicking `File` > `New` > `Terminal` from the top menu.

Run the following command in **terminal**:
`cd ~/work/git-intro/2/ && mv git .git`

**Note:** To copy and paste: use **Control-C** and to paste inside of a terminal, use **Control-V**

You can access lab at `<host-ip>:<port>/lab/workspaces/lab2`

### Step 1 - Git Status
`git status` allows us to view the changes in the working directory and staging area compared to the repository.

Given the current repository running `git status` displays that a change has been made in our working directory to a previously committed file, committed.js, but has not yet been moved to the staging area.

### Step 2 - Git Diff
The command `git diff` enables you to compare changes in the working directory against a previously committed version. By default the command compares the working directory and the HEAD commit.

If you wish to compare against an older version then provide the commit hash as a parameter, for example git diff <commit>. Comparing against commits will output the changes for all of the files modified. If you want to compare the changes to a single file then provide the name as an argument such as `git diff committed.js`.

**Protip**

By default the output is in the combined diff format. The command git difftool will load an external tool of your choice to view the differences.

### Step 3 - Git Add
As in the previous scenario in order to commit a change it must first be staged using git add command.

**Task**

To proceed first stage your changes using **git add**

**Protip**

If you rename or delete files then you need to specify these files in the add command for them to be tracked. Alternatives you can use git mv and git rm for git to perform the action and include update the staging area.

**Solution**

`git add committed.js`

### Step 4 - Staged Differences
Once the changes are in the staging area they will not show in the output from `git diff` . By default, git diff will only compare the working directory and not the staging area.

To compare the changes in the staging area against the previous commit you provide the staged parameter `git diff --staged`. This enables you to ensure that you have correctly staged all your changes.


### Step 5 - Git Log
The command git log allows you to view the history of the repository and the commit log.

**Protip**

The format of the log output is very flexible. For example to output each commit on a single line the command is `git log --pretty=format:"%h %an %ar - %s"`.

### Step 6 - Git Show
While git log tells you the commit author and message, to view the changes made in the commit you need to use the the command:

`git show`

Like with other commands, by default it will show the changes in the HEAD commit. Use `git show <commit-hash>` to view older changes. You can get commit-id from **git log** command output and use it with **git show** command.
