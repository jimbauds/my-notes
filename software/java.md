# Java

## Installing Java JRE 7 under Debian 6 (Docker)
```sh
# Start a new container
sudo docker run -it debian:6.0.10 /bin/bash

# Udpate the container
apt-get udpate
apt-get upgrade

# Install wget
apt-get install wget

# Download JRE 7

# Create runtime directory
mkdir -p /usr/lib/jvm

# Uncompress
tar -xzf jre.tar.gz -C /usr/lib/jvm

# Inform system about the new Java
update-alternatives --install "/usr/bin/java" "java" "/usr/lib/jvm/jre1.7.0_67/bin/java" 1

# Set default
update-alternatives --set java /usr/lib/jvm/jre1.7.0_67/bin/java

# Test Java
java -version
```
