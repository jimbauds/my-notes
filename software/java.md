# Java

## Installing Java JRE 7 under Debian 6
```sh
# Start a new container
sudo docker run -it debian:6.0.10 /bin/bash

# Udpate the container
apt-get udpate
apt-get upgrade

# Install wget
apt-get install wget

# Download JRE 7
wget http://download.oracle.com/otn-pub/java/jdk/7u67-b01/jre-7u67-linux-x64.tar.gz?AuthParam=1408244145_290535ed0dc3d2356f0b7e7de3c94c19

# Rename the file
mv jre-7u67-linux-x64.tar.gz?AuthParam=1408244145_290535ed0dc3d2356f0b7e7de3c94c19 jre.tar.gz

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
