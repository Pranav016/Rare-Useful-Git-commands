# Git commands

-   `git restore .` - restores the files to the previous commit/ undos all the local changes that haven't been commited.

-   `git restore index.html` - restores only that particular file to the recent commit/ undos all the local/uncommited changes for that file.

-   `git reset --hard <hash code of the commit>` - removes commits and goes back to the commit for that hash code

-   `git reset --source <hash code> index.html>`- removes commits and goes back to the commit for that hash code only for that particular file.

-   `git commit --amend -m 'Your message'`- helps re-write messages

-   `git revert <hash code>`- helps to roll back to a previous commit by creating a new commit for it. Doesn't removes those commits from the `log` like `git reset` does.

-   `git reflog`- this can be useful to bring back deleted commits/files/changes. Use `git reset <hash code of lost commit from reflog>` to bring back rolled changes.

-   `git reset HEAD~2`- Helps roll back by 2 commits and unstage all the changes in those 2 commits removed.

-   `git rebase`-

## Moving commited changes to a new branch: (scenario: you accidently worked on master)

-   -   Use `git checkout -b new-feature`
-   -   Then roll back commits on master using `git reset HEAD~1 --hard`-> (this command will roll back 1 commit)

## stashing-

-   `git stash`

    -   stashes/ saves the changes in the back of the project/ another directory of the project and the control moves back to the last working copy of the last commit.
    -   saves the changes as a draft and moves back to code of the last commit

-   `git stash list` - lists all the draft changes in the back of the project

-   `git stash pop`- pops the draft changes back into the working directory/ on the working branch

-   `git stash clear`- clears/ deletes all the draft changes stored

## Moving commited changes to an already existing branch using cherry-pick:

-   -   `git checkout feature-branch`
-   -   `git cherry-pick <hash code of that commit on master>`
-   -   `git checkout master`
-   -   `git reset HEAD~1 --hard` (rolls back 1 commit)

## Squashing commits-
