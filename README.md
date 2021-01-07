# GitCookbook
- [GitCookbook](#GitCookbook)
    * [Recipes](#Recipes)
        + [Diff commits or a particular file](#Diff-commits-or-a-particular-file)
        + [Diff commits or a particular file](#Test-with-spaces)
## Recipes
### Diff commits or a particular file
```bash
git diff HEAD^ HEAD # diff between last version and current
git difftool HEAD^ HEAD # diff between last version and current - only if you configured a diff tool
git diff @{upstream} # diff local branch with the upstream branch (if you're on the branch)
git diff <remote-tracking branch> <local branch> [<file>] # diff remote file with the local one
```
### View commit history
```bash
git log --oneline # show commits in a concise form
git log --all --decorate --oneline --graph # show commit graph including branches (a dog - woof!)
```
### View file
```bash
git show HEAD:<file> # view file in head revision.
git log -p --follow <filename> # show file history through the commit history; --follow - include renames, -p - also diff
```


```bash
# add existing local repository to the remote one
git init # create .git stuff
git add . # add all the files
git commit -m "first commit"
git remote add <name (usually origin)> <url> # connect to remote
git push -u origin master # -u is the same as --set-upstream

# global commit and push
git commit -a -m "<desc>" # -a == -all - automatically stage files that have been modified and deleted, but new files you have not told Git about are not affected
git push

# untrack
# remove hidden .git folder

# get remote repo
git clone <url>

# discard all local changes (get back to the last commit)
git reset --hard

# reset single file to the latest commit
git checkout <file> # in local repo
git checkout origin/master -- path/to/file # in remote repo

# remove local untracked files
git clean -f -d -x # -f files, -d dirs, -x ignored and non-ignored, -X ignored, add -n to see which files will be deleted

# remove files from index
git rm -r --cached . # -r - recursive removal, --cached - only index (without working tree), add -n to preview removal first.

# view staged and non-staged files
git status

# simple branching and merging
git branch --all # show all branches
git branch -vv # same as above but local and corresponding upstream remote is printed on one line
git checkout -b newBranch # create a new branch from the active one and switch to it at the same time
git commit -a -m "newBranch finished and tested."
git push -u origin newBranch # push the newBranch branch to the remote repository and set it as upstream
git checkout master # return to the master branch
# Note: above command doesn't set the corresponding remote as upstream. For example, git diff @{upstream}
# now compares HEAD with remotes/origin/newBranch instead of remotes/origin/master until you switch upstream
git branch -u remotes/origin/master # set remotes/origin/master as upstream
git merge newBranch # merge the newBranch branch back into the master branch
git commit -a -m "merged with newBranch" # you need to commit if the merge was fast-forward
git push -u origin master # set remotes/origin/master as upstream (if not set yet) and push
git push origin --delete newBranch # delete the remote branch
git branch -d newBranch # delete the local branch because there's no further need for it
git log --all --decorate --oneline --graph # show branching graph

# change user name and email
git config --global user.name 'Anonymous'
git config --global user.email '<>'

# get remote changes
git fetch # download objects and refs from remote
git diff HEAD remotes/origin/HEAD # diff local HEAD with just fetched remote HEAD
git merge remotes/origin/HEAD # merge with what was fetched
# or just
git pull # equivalent of git fetch && git merge

# clone repo to non-empty directory
# Clone just the repository's .git folder (excluding files as they are already in
# `existing-dir`) into an empty temporary directory
git clone --no-checkout repo-to-clone existing-dir/existing-dir.tmp # might want --no-hardlinks for cloning local repo
# Move the .git folder to the directory with the files.
# This makes `existing-dir` a git repo.
mv existing-dir/existing-dir.tmp/.git existing-dir/
# Delete the temporary directory
rmdir existing-dir/existing-dir.tmp
cd existing-dir
# Download existing files
git checkout
```
### Test with spaces

- [Heading](#heading)
  * [Sub-heading](#sub-heading)
    + [Sub-sub-heading](#sub-sub-heading)
- [Heading](#heading-1)
  * [Sub-heading](#sub-heading-1)
    + [Sub-sub-heading](#sub-sub-heading-1)
- [Heading](#heading-2)
  * [Sub-heading](#sub-heading-2)
    + [Sub-sub-heading](#sub-sub-heading-2)


# Heading levels

> This is a fixture to test heading levels

<!-- toc -->

## Heading

This is an h1 heading

### Sub-heading

This is an h2 heading

#### Sub-sub-heading

This is an h3 heading

## Heading

This is an h1 heading

### Sub-heading

This is an h2 heading

#### Sub-sub-heading

This is an h3 heading

## Heading

This is an h1 heading

### Sub-heading

This is an h2 heading

#### Sub-sub-heading

This is an h3 heading
