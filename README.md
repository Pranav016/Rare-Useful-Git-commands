# Git commands
- `git restore .` - restores the files to the previous commit/ undos all the local changes that haven't been commited.

- `git restore index.html` - restores only that particular file to the recent commit/ un do's all the local/uncommited changes for that file.

- `git reset --hard <hash code of the commit>` - removes commits and goes back to the commit for that hash code

- `git reset --source <hash code> index.html>`- removes commits and goes back to the commit for that hash code only for that particular file.

- `git commit --amend -m 'Your message'`- helps re-write messages

- `git revert <hash code>`- helps to roll back to a previous commit by creating a new commit for it. Doesn't removes those commits from the `log` like `git reset` does.

- `git reflog`- this can be useful to bring back deleted commands. Use `git reset <hash code of lost commit from reflog>` to bring back rolled changes. 

## Moving commited changes to a new branch-
- - Use `git branch new-feature`
- - Then roll back commits on master using `git reset HEAD~1 --hard`-> (this command will roll back 1 commit)
