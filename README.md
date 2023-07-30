## Git commands

-   `git restore .` - restores the files to the previous commit/ undos all the local changes that haven't been committed.
<br/>

-   `git restore index.html` - restores only that particular file to the recent commit/ undos all the local/uncommitted changes for that file.
<br/>

-   `git reset --hard <hash code of the commit>` - removes commits and goes back to the commit for that hash code
<br/>

-   `git checkout <hash code of the commit> -- <path/to/file>`- goes back to the commit with that hash code only for that particular file. You need to create a new commit after the rollback is complete.
<br/>

-   `git commit --amend -m 'Your message'`- helps re-write messages
<br/>

-   `git revert <hash code>`- helps to roll back to a previous commit by creating a new commit for it. Doesn't removes those commits from the `log` like `git reset` does.
<br/>

-   `git reflog`- this can be useful to bring back deleted commits/files/changes. Use `git reset <hash code of lost commit from reflog>` to bring back rolled changes.
<br/>

-   `git reset HEAD~2`- Helps roll back by 2 commits and unstage all the changes in those 2 removed commits.
<br/>

-   `git reset HEAD~2 --hard` - Helps roll back by 2 commits but permanently removes all the changes in those 2 removed commits.
<br/>

-   `git rebase` (most useful command)- Reapply commits on top of another base tip. ex. `git rebase master` sets the branch at the tip of master branch
<br/>

## Solution to difficult scenarios while using Git:
<br/>

### 1. Moving committed changes to a new branch: (scenario: you accidentally worked on master)

-   -   Use `git checkout -b new-feature`
-   -   Then roll back commits on master using `git reset HEAD~1 --hard`: (this command will roll back 1 commit)
<br/>

### 2. Stashing (example scenario: you need to work/switch on a new branch without making a commit on the current branch)
<br/>

##### All about git stashing:
-   Use `git stash` when you want to record the current state of the working directory and the index, but want to go back to a clean working directory. The command saves your local modifications away and reverts the working directory to match the HEAD commit.
-   The modifications stashed away by this command can be listed with `git stash list`, inspected with `git stash show`, and restored (potentially on top of a different commit) with `git stash apply`. Calling `git stash` without any arguments is equivalent to `git stash push`.
<br/>

*   `git stash`

    -   stashes/ saves the changes in the back of the project/ another directory of the project and the control moves back to the last working copy of the last commit.
    -   saves the changes as a draft and moves back to code of the last commit.
<br/>

*   `git stash push -m "Message"`- Adds a message for the stash to the stash list
<br/>

*   `git stash list` - lists all the draft changes in the back of the project
    **Tip-** The stash list stores all the stashes and each stashed feature/code has a unique index number to it. The last added stash always appears at the top with index 0.
<br/>

*   `git stash apply` - applies the last stashed draft to our current working directory
<br/>

*   `git stash apply <index number>` - applies the particular indexed stash to our current working directory
<br/>

*   `git stash drop <index number>` - drops the stash out of the stash list with the particular index
<br/>

*   `git stash pop`- pops the last draft changes back into the working directory/ on the working branch and that draft is then removed from the stash list
<br/>

*   `git stash pop <index number>`- pops the draft change with the particular index back into the working directory/ on the working branch and that draft is then removed from the stash list
<br/>

*   `git stash clear`- clears/ deletes all the draft changes stored

#### Final Solution using stashing-
-   -   First add all changes to staging using `git add .`
-   -   Stash changes using `git stash` command.
-   -   Go to your new branch and use command `git stash apply`.

<br/>

### 3. Moving committed changes to an already existing branch using cherry-pick(scenario: you accidently worked on master when there is already a dedicated branch for the feature):

-   -   `git checkout feature-branch`
-   -   `git cherry-pick <hash code of that commit on master>`
-   -   `git checkout master`
-   -   `git reset HEAD~1 --hard` (rolls back 1 commit)

**Note-**
This scenario can also be solved using the stashing method explained in #2. You can stash changes and apply those changes to new branch using `git stash apply`.
<br/>

<br/>

### 4. Squashing commits (scenario: you made a bunch of extra commits because of errors and you wan to combine commits into one with a new commit message)-

-   `git rebase -i <hash code of the commit above which all the commits need to be squashed>`
    -   i stands for interactive squash
    -   opens up squashing in vim editor where you can pick or squash and update commit messages.
<br/>

### 5. Bisect (scenario: there is a bug introduced in the code but you don't know which commit introduced the bug)-
- Uses binary search to find the commit that introduced a bug.

#### Procedure-

1. `git bisect start`- starts the searching procedure to find the bad commit.

1. (Optional) Use the command `git bisect good <hash-code of the commit that you are sure doesn't have the bug>`- usually this is the first or the second commit and tells git to start from the middle.

1. git will start checking out commits on its own, you have to test the commit and let git know if the commit has the bug or not by using commands, 
  - `git bisect good`- if the commit is fine
  - `git bisect bad`- if the commit has the bug.

1. After giving feedbacks, git has a feedback tree that it uses to return the commit that introduced the bug/ the first bad commit, you can copy its hash code. The reference `refs/bisect/bad` will be left pointing at that commit.

1. After a bisect session, to clean up the bisection state and return to the original HEAD, issue the following command:

1. `git bisect reset`- By default, this will return your tree to the commit that was checked out before git bisect start.

1. `git bisect reset <commit>`- For example, `git bisect reset bisect/bad` will check out the first bad revision, while `git bisect reset HEAD` will leave you on the current bisection commit and avoid switching commits at all.

1. `git revert <hash-code of the bad commit>`- used to revert the changes done in the bad commit that introduced the bug in the code.
<br/>

### 6. Filter branch (scenario: You want to remove a particular file, whether a large file or any api key accidently uploaded, from you previous commits)-

```
git filter-branch --index-filter 'git rm --cached --ignore-unmatch filepath' HEAD
```

- Rewrites whichever commit has the particular file present in it while removing it from the commit.
- Starts searching from `HEAD` commit.
- `--ignore-unmatch` helps avoiding errors if file is not found.
- Commit time and other properties remain same, only SHA/ Hash of the commit may update if the particular file is found and removed from that commit.

### 7. Your commits aren't appearing on your GitHub graph:
- This mostly happens when either the username or email set in the `.gitconfig` file in your system is different than the username and email on your GitHub account.

<br/>

**Solution-**

```
git filter-branch --env-filter '
if [ "$GIT_COMMITTER_EMAIL" = "<Old Email>" ];
        then
                GIT_COMMITTER_NAME="<New Name>";
                GIT_AUTHOR_NAME="<New Name>";
                GIT_COMMITTER_EMAIL="<New Email>";
                GIT_AUTHOR_EMAIL="<New Email>";
                git commit-tree "$@";
        else
                git commit-tree "$@";
        fi' HEAD
```

<br/>

### 8. Resetting a particular file to HEAD/ removing the new changes added to a particular file.

<br/>

- Use command `git checkout HEAD -- <file-name>` to reset the changes done in a particular file back to its state in the last commit.

<br/>

<hr/>

## Bonus command-
### Creating zip files using git:
```
git archive --format=zip --output project.zip master
```
This command will output a zip file for master branch and will not include files mentioned in `.gitignore`.

<hr/>

## Connect with me-
- [GitHub](https://github.com/Pranav016)
- [LinkedIn](https://www.linkedin.com/in/pranav-mendiratta/)
