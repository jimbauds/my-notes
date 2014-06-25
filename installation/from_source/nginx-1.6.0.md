# Nginx: Installation from source (Debian 7 Wheezy)

### (Optional) Docker container creation:

You can run the server into a docker container for isolation purpose. If you don't know what docker is all
about, take a look at [docker.io](http://docker.io).

Create a new container with this command:
`docker run -i -t -p 80:80 --name='<container_name>' debian bash`

This is going to run a container based on Debian GNU/Linux latest version. The port 80 is going to be bind to the port 80
of the host.


