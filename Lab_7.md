# Lab: Git submodules

Git submodules allow you to keep a git repository as a subdirectory of
another git repository. Git submodules are simply a reference to another
repository at a particular snapshot in time. Git submodules enable a Git
repository  to incorporate and track version history of external code.


Common commands for git submodules
----------------------------------

### Add git submodule

The `git submodule add` is used to add a new
submodule to an existing repository. The following is an example that
creates an empty repo and explores git submodules.

```
    $ mkdir git-submodule-demo
    $ cd git-submodule-demo/
    $ git init
    Initialized empty Git repository in /Users/atlassian/git-submodule-demo/.git/
```

This sequence of commands will create a new directory
`git-submodule-demo`, enter that directory,
and initialize it as a new repository. Next we will add a submodule to
this fresh new repo.

```
    $ git submodule add https://github.com/fenago/gitdemo
    Cloning into '/Users/atlassian/git-submodule-demo/gitdemo'...
    remote: Counting objects: 8, done.
    remote: Compressing objects: 100% (6/6), done.
    remote: Total 8 (delta 1), reused 0 (delta 0)
    Unpacking objects: 100% (8/8), done.
```

The `git submodule add` command takes a URL
parameter that points to a git repository. Here we have added the
`gitdemo` as a submodule. Git will
immediately clone the submodule. We can now review the current state of
the repository using `git status`\...

```
    $ git status
    On branch main

    No commits yet

    Changes to be committed:
      (use "git rm --cached <file>..." to unstage)

     new file:   .gitmodules
     new file:   gitdemo
```

There are now two new files in the repository `.gitmodules` and the `gitdemo`
directory. Looking at the contents of `.gitmodules` shows the new submodule mapping

```
    [submodule "gitdemo"]
     path = gitdemo
     url = https://github.com/fenago/gitdemo
```


```
    $ git add .gitmodules gitdemo/
    $ git commit -m "added submodule"
    [main (root-commit) d5002d0] added submodule
     2 files changed, 4 insertions(+)
     create mode 100644 .gitmodules
     create mode 160000 gitdemo
```

### Submodule workflows

Once submodules are properly initialized and updated within a parent
repository they can be utilized exactly like stand-alone repositories.
This means that submodules have their own branches and history. When
making changes to a submodule it is important to publish submodule
changes and then update the parent repositories reference to the
submodule. Let's continue with the `gitdemo` example and make some changes:

```
    $ cd gitdemo/
    $ git checkout -b new_awesome
    Switched to a new branch 'new_awesome'
    $ echo "new awesome file" > new_awesome.txt
    $ git status
    On branch new_awesome
    Untracked files:
      (use "git add <file>..." to include in what will be committed)

     new_awesome.txt

    nothing added to commit but untracked files present (use "git add" to track)
    $ git add new_awesome.txt
    $ git commit -m "added new awesome textfile"
    [new_awesome 0567ce8] added new awesome textfile
     1 file changed, 1 insertion(+)
     create mode 100644 new_awesome.txt
    $ git branch
      main
    * new_awesome
```

Here we have changed directory to the gitdemo submodule. We have
created a new text file `new_awesome.txt`
with some content and we have added and committed this new file to the
submodule. Now let us change directories back to the parent repository
and review the current state of the parent repo.

```
    $ cd ..
    $ git status
    On branch main
    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)

     modified:   gitdemo (new commits)

    no changes added to commit (use "git add" and/or "git commit -a")
```

Executing `git status` shows us that the
parent repository is aware of the new commits to the
`gitdemo` submodule. It doesn\'t go
into detail about the specific updates because that is the submodule
repositories responsibility. The parent repository is only concerned
with pinning the submodule to a commit. Now we can update the parent
repository again by doing a `git add` and
`git commit` on the submodule. This will put
everything into a good state with the local content. If you are working
in a team environment it is critical that you then `git push` the submodule updates, and the parent repository
updates.

When working with submodules, a common pattern of confusion and error is
forgetting to push updates for remote users. If we revisit the
`gitdemo` work we just did, we pushed
only the updates to the parent repository. Another developer would go to
pull the latest parent repository and it would be pointing at a commit
of `gitdemo` that they were unable to
pull because we had forgotten to push the submodule. This would break
the remote developers local repo. To avoid this failure scenario make
sure to always commit and push the submodule and parent repository.

Conclusion
----------

Git submodules are a powerful way to leverage git as an external
dependency management tool. Weigh the pros and cons of git submodules
before using them, as they are an advanced feature and may take a
learning curve for team members to adopt.
