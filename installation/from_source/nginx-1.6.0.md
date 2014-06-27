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
apt-get install curl gcc make g++ openssl libpcre3-dev wget
```

Create a new directory for holding source files  
```
mkdir assets
cd assets
```

**zlib Installation**  
```
curl -O http://zlib.net/zlib-1.2.8.tar.gz
gzip -d zlib-1.2.8.tar.gz
tar -xf zlib-1.2.8.tar
cd zlib-1.2.8
./configure
make
make install
cd ..
rm -rf zlib-1.2.8
```

# Nginx Installation
```
curl -O http://nginx.org/download/nginx-1.6.0.tar.gz
gzip -d nginx-1.6.0.tar.gz
tar -xf nginx-1.6.0.tar
cd nginx-1.6.0
./configure
make
make install
cd ..
rm -rf nginx-1.6.0
```

  nginx path prefix: "/usr/local/nginx"
  nginx binary file: "/usr/local/nginx/sbin/nginx"
  nginx configuration prefix: "/usr/local/nginx/conf"
  nginx configuration file: "/usr/local/nginx/conf/nginx.conf"
  nginx pid file: "/usr/local/nginx/logs/nginx.pid"
  nginx error log file: "/usr/local/nginx/logs/error.log"
  nginx http access log file: "/usr/local/nginx/logs/access.log"
  nginx http client request body temporary files: "client_body_temp"
  nginx http proxy temporary files: "proxy_temp"
  nginx http fastcgi temporary files: "fastcgi_temp"
  nginx http uwsgi temporary files: "uwsgi_temp"
  nginx http scgi temporary files: "scgi_temp"


**Service script**
wget https://raw.github.com/JasonGiedymin/nginx-init-ubuntu/master/nginx -O /etc/init.d/nginx
chmod +x /etc/init.d/nginx

service nginx status  # to poll for current status
service nginx stop    # to stop any servers if any
service nginx start   # to start the server


### Config file

