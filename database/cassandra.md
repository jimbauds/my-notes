# Apache Cassandra

## Requirements
  * Java 7 64bits Server Edition
  * Python 2.5+ (Cassandra Tools)
  * Cassandra Cluster Manager (CCM)

## Installation
```sh
# Install Java jre 7u67
sudo rm -rf /usr/lib/jvm
sudo mkdir /usr/lib/jvm
sudo tar -xzf server-jre-7u67-linux-x64.tar.gz -C /usr/lib/jvm
sudo update-alternatives --install "/usr/bin/java" "java" "/usr/lib/jvm/jdk1.7.0_40/bin/java" 1
sudo update-alternatives --set java /usr/lib/jvm/jdk1.7.0_40/bin/java

# Install JNA
sudo apt-get install libjna-java

# Download latest Apache Cassandra (DataStax Comunity Edition)
wget http://downloads.datastax.com/community/dsc.tar.gz

# Untar
tar -xzf dsc.tar.gz
```

## Package Installation Default Folder
```sh
/var/lib/cassandra #=> Data directories
/var/log/cassandra #=> Log directory
/var/run/cassandra #=> Runtime files
/usr/share/cassandra #=> Environment settings
/usr/share/cassandra/lib #=> JAR files
/usr/bin #=> Binary files
/usr/sbin
/etc/cassandra #=> Configuration files
/etc/init.d #=> Service startup script
/etc/security/limits.d #=> Cassandra user limits
/etc/default
```
