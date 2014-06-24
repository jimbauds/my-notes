# Docker

### Installation (Debian/Ubuntu) 64bits
```shell
echo deb https://get.docker.io/ubuntu docker main > /etc/apt/sources.list.d/docker.list
apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 36A1D7869245C8950F966E92D8576A8BA88D21E9
apt-get update
apt-get install lxc-docker

#Optional
usermod -a -G docker [username] #=> add yourself to the docker group
sg docker #=> switch to that group
```

### Basic commands:
```shell
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
```shell
sudo docker run -i -t ubuntu bash
# Make changes to the image and exit the container
sudo docker ps -a
sudo docker commit -m "MyImage" <ID> <NewName>
```

### Save an image to a tar archive:
```shell
sudo docker save busybox > busybox.tar
```
### Load an image from a tar file:
```shell
sudo docker load < busybox.tar
# or
sudo docker load --input fedora.tar
```

### Export the contents of a filesystem as a tar archive to STDOUT:
```
sudo docker export red_panda > latest.tar
```
