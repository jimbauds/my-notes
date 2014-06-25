# Nginx: Installation from source (Debian 7 Wheezy)

### Docker container creation (Optional):

You can run the server into a docker container for isolation purpose. If you don't know what docker is all
about, take a look at [docker.io](http://docker.io).

Create a new container with this command:
```
docker run -i -t -p 80:80 --name='<container_name>' debian bash
```
This is going to run a container based on Debian GNU/Linux latest version. The port 80 is going to be bind to the port 80
of the host.

Inside the container, you can install everything else like a normal host. Once finished, you commit the container to a new image to save the change
```
sudo docker commit -m "<commit_message>" <container_id> <new_image_name>
```

### Prerequisites installation:

First you need to update the server to the latest version:
```
sudo apt-get update
sudo apt-get upgrade
```
Now you can install the prerequisite:
```

```
