# Apache Cassandra Cluster

```sh
# Update System
sudo apt-get update
sudo apt-get upgrade

# Install Java SE 7u67 server

# Get Cassandra
wget http://apache.mirror.rafal.ca/cassandra/2.0.9/apache-cassandra-2.0.9-bin.tar.gz
tar -xzf apache-cassandra-2.0.9-bin.tar.gz

# Make/Partition/Mount Cassandra Data folder from second HDD
sudo mkdir /cassandra_data

# WARNING: Only for new disk. 
# DO NOT partition if the disk already contain data.
# Mount the disk directly instead.
sudo mke2fs -F -F -O ^has_journal -t ext4 -b 4096 -E lazy_itable_init=0 /dev/sdb

# Mount the disk
sudo mount /dev/sdb /cassandra_data
sudo chmod a+w /cassandra_data

```

## To Classified
```sh
# For listing open file
sudo apt-get install lsof
lsof /

# Check disk and partition
sudo lsblk -o NAME,FSTYPE,SIZE,MOUNTPOINT,LABEL
```
