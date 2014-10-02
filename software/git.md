# Git Commands

## How to put a Bare Repository to a Remote Server
```sh
git clone --bare my_project my_project.git # Clone the Project into a Bare Repository
scp -r my_project.git user@server:/opt/git # Put the Bare Repository to a Server
```
## How to commit to the last commit
```sh
git add <file>
...
git commit --amend
```
## How to reset a file
```sh
git checkout -- <file> # Discard changes for a file
git reset --hard # Discard all changes on all files. Going back to the last commit before the changes.
git revert <commitid> # Revert a commit and do a new commit
```
