# Git Commands

### How to put a Bare Repository to a Remote Server:
```shell
git clone --bare my_project my_project.git #=> Clone the Project into a Bare Repository
scp -r my_project.git user@server:/opt/git #=> Put the Bare Repository to a Server
```
