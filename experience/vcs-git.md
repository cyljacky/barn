# VCS - Git

There should have many type of distributed workflow. This note should focus on Subversion-Style Workflow, i.e.:

Other workflow example please check [here](https://git-scm.com/about/distributed)

## Terminology

### Repository

In simplified version, it means the project that is under the git control.

Detailed explanation, is the object database of the project, storing everything from the files themselves, to the versions of those files, commits, deletions, etc.

### Remote / Origin

Origin is conventional name for the primary version of a repository. Mostly means the repository copy that's in the centralised server\(e.g. gitlab, github\).

Remote means the repository copy from the Origin, e.g. the copy that in developer's local server.

Remote can interact with Origin, to sync the progress of the repository.

### Commit

A node of git repository, which stores a snapshot in the history of the repository.

### Branch

A version of the repository that diverges from the main working project on any purpose, e.g. new feature, bugfix, testing, etc.

## Command

### git remote

`git remote set-url origin <new.git.url/here>` Assign git repository url to current directory. This case usually used to update or mark the origin repository's location.

### git status

check status of the repository

```bash
$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
```

### git diff

`git diff <filepath list>`

compare the file with it's previous commit.  
if not any filename input will list out all file difference.

```bash
$ git diff README.md
diff --git a/README.md b/README.md
index f6976b1..9d17585 100644
--- a/README.md
+++ b/README.md
@@ -1,5 +1,5 @@
some common content
-
+new added contect
more common content
```

### git checkout

`git checkout [-b] [origin/]<branch name>`

used to switch branch, file update may be keep.

`-b` flag used to create new branch before switch to it. `origin/` used to

```bash
$ git checkout origin/master
M    README.md
Note: checking out 'origin/master'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by performing another checkout.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -b with the checkout command again. Example:

  git checkout -b <new-branch-name>

HEAD is now at 59e5476 Merge branch 'branch-for-stage' into 'master'
```

### git add

`git add <filepath list>`

prepare files listed into staged list, which is pending to commit.

wildcard \(\*\) is supported

### git commit

`git commit [-- <filepath list>]`

Create a commit containing the current contents of the index and the given log message describing the changes.

Editor will revealed to input the commit message.

### git push

For no branch in origin case:

```bash
$ git push
fatal: The current branch test-git has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin test-git
```

## Reference

- [https://linuxacademy.com/blog/linux/git-terms-explained](https://linuxacademy.com/blog/linux/git-terms-explained) 
- [https://www.atlassian.com/git/glossary/terminology](https://www.atlassian.com/git/glossary/terminology)

