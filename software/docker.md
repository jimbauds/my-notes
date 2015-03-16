# Docker

### Commands
```sh
# Source: https://www.calazan.com/docker-cleanup-commands/
# Kill all running containers
docker kill $(docker ps -q)
# Delete all stopped containers (including data-only containers)
docker rm $(docker ps -a -q)
# Delete all ‘untagged/dangling’ (<none>) images
docker rmi $(docker images -q -f dangling=true)
# Delete ALL images
docker rmi $(docker images -q)
# Alias
# ~/.bash_aliases

# Kill all running containers.
alias dockerkillall='docker kill $(docker ps -q)'

# Delete all stopped containers.
alias dockercleanc='printf "\n>>> Deleting stopped containers\n\n" && docker rm $(docker ps -a -q)'

# Delete all untagged images.
alias dockercleani='printf "\n>>> Deleting untagged images\n\n" && docker rmi $(docker images -q -f dangling=true)'

# Delete all stopped containers and untagged images.
alias dockerclean='dockercleanc || true && dockercleani'
```


### Installation
```sh
# Debian 7.5 (Kernel must be 3.8+)
echo deb https://get.docker.io/ubuntu docker main > /etc/apt/sources.list.d/docker.list
apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 36A1D7869245C8950F966E92D8576A8BA88D21E9
# Sometimes
apt-get install apt-transport-https

apt-get update
apt-get install lxc-docker

# CentOS 7 (official)
sudo yum install docker
sudo service docker start
sudo chkconfig docker on

# CentOS 7 (EPEL Repos)
curl -O http://dl.fedoraproject.org/pub/epel/beta/7/x86_64/epel-release-7-0.2.noarch.rpm
sudo rpm -ivh epel-release-7-0.2.noarch.rpm
sudo yum install docker-io
sudo service docker start
sudo chkconfig docker on

#Optional
usermod -a -G docker [username] #=> add yourself to the docker group
sg docker #=> switch to that group
```
### Basic commands:
```sh
sudo docker ps #=> Show currently running docker containers
sudo docker ps -a #=> Show currently running and past docker containers
sudo docker version
sudo docker info
sudo docker images
sudo docker run -i -t ubuntu bash #=> Create a new container based on ubuntu
sudo docker diff
sudo docker rm <ContainerID> #=> Remove a container
sudo docker logs <ContainerID>
sudo docker attach <ContainerID>
sudo docker inspect <ContainerID>
sudo docker start <ContainerID>
sudo docker stop <ContainerID>
```
### Create docker image:
```sh
sudo docker run -i -t ubuntu bash
# Make changes to the image and exit the container
sudo docker ps -a
sudo docker commit -m "MyImage" <ID> <NewName>
```
### Save an image to a tar archive:
```sh
sudo docker save busybox > busybox.tar
```
### Load an image from a tar file:
```sh
sudo docker load < busybox.tar
# or
sudo docker load --input fedora.tar
```
### Export the contents of a filesystem as a tar archive to STDOUT:
```sh
sudo docker export red_panda > latest.tar
```
### Volumes
```sh
sudo docker run -it -v /$(pwd)/<host_folder>:/<container_folder> debian bash
docker run -d -v /dbdata --name dbdata training/postgres
docker run -d --volumes-from dbdata --name db1 training/postgres
docker run -d --volumes-from dbdata --name db2 training/postgres
docker run -d --name db3 --volumes-from db1 training/postgres
sudo docker run --volumes-from dbdata -v $(pwd):/backup ubuntu tar cvf /backup/backup.tar /dbdata
```
### Extras:
To detach the tty without exiting the shell, use the escape sequence Ctrl-p + Ctrl-q
