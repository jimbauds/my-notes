# Git Commands

## How to put a Bare Repository to a Remote Server:
```sh
git clone --bare my_project my_project.git #=> Clone the Project into a Bare Repository
scp -r my_project.git user@server:/opt/git #=> Put the Bare Repository to a Server
```
## How to commit to the last commit
```sh
git add <filename>
git commit --amend
```
