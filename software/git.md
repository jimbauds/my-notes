# Git Commands

### How to put a Bare Repository to a Remote Server:
```shell
# Clone the Project into a Bare Repository
git clone --bare my_project my_project.git

# Put the Bare Repository on a Server
scp -r my_project.git user@server:/opt/git 
```
