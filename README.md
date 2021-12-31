# Git commands

-   `git restore .` - restores the files to the previous commit/ undos all the local changes that haven't been commited.

-   `git restore index.html` - restores only that particular file to the recent commit/ undos all the local/uncommited changes for that file.

-   `git reset --hard <hash code of the commit>` - removes commits and goes back to the commit for that hash code

-   `git reset --source <hash code> index.html>`- removes commits and goes back to the commit for that hash code only for that particular file.

-   `git commit --amend -m 'Your message'`- helps re-write messages

-   `git revert <hash code>`- helps to roll back to a previous commit by creating a new commit for it. Doesn't removes those commits from the `log` like `git reset` does.

-   `git reflog`- this can be useful to bring back deleted commits/files/changes. Use `git reset <hash code of lost commit from reflog>` to bring back rolled changes.

-   `git reset HEAD~2`- Helps roll back by 2 commits and unstage all the changes in those 2 removed commits.

-   `git reset HEAD~2 --hard`

-   `git rebase` (most useful command)- Reapply commits on top of another base tip. ex. `git rebase master` sets the branch at the tip of master branch

## Moving commited changes to a new branch: (scenario: you accidently worked on master)

-   -   Use `git checkout -b new-feature`
-   -   Then roll back commits on master using `git reset HEAD~1 --hard`: (this command will roll back 1 commit)

## stashing-

-   Use `git stash` when you want to record the current state of the working directory and the index, but want to go back to a clean working directory. The command saves your local modifications away and reverts the working directory to match the HEAD commit.
-   The modifications stashed away by this command can be listed with `git stash list`, inspected with `git stash show`, and restored (potentially on top of a different commit) with `git stash apply`. Calling `git stash` without any arguments is equivalent to `git stash push`.

*   `git stash`

    -   stashes/ saves the changes in the back of the project/ another directory of the project and the control moves back to the last working copy of the last commit.
    -   saves the changes as a draft and moves back to code of the last commit

*   `git stash push -m "Message"`- Adds a message for the stash to the stash list

*   `git stash list` - lists all the draft changes in the back of the project
    **Tip-** The stash list stores all the stashes and each stashed feature/code has a unique index number to it. The last added stash always appears at the top with index 0.

*   `git stash apply` - applies the last stashed draft to our current working directory

*   `git stash apply <index number>` - applies the particular indexed stash to our current working directory

*   `git stash drop <index number>` - drops the stash out of the stash list with the particular index

*   `git stash pop`- pops the last draft changes back into the working directory/ on the working branch and that draft is then removed from the stash list

*   `git stash pop <index number>`- pops the draft change with the particular index back into the working directory/ on the working branch and that draft is then removed from the stash list

*   `git stash clear`- clears/ deletes all the draft changes stored

## Moving commited changes to an already existing branch using cherry-pick:

-   -   `git checkout feature-branch`
-   -   `git cherry-pick <hash code of that commit on master>`
-   -   `git checkout master`
-   -   `git reset HEAD~1 --hard` (rolls back 1 commit)

## Squashing commits-

-   `git rebase -i <hash code of the commit above which all the commits need to be squashed>`
    -   i stands for interactive squash
    -   opens up squashing in vim editor where you can pick or squash and update commit messages
