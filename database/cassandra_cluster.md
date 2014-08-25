# Apache Cassandra Cluster

```sh
sudo apt-get update
sudo apt-get upgrade

# Install Java SE 7u67 server

wget http://apache.mirror.rafal.ca/cassandra/2.0.9/apache-cassandra-2.0.9-bin.tar.gz
tar -xzf apache-cassandra-2.0.9-bin.tar.gz

# Make/Partition/Mount Cassandra Data folder from second HDD
sudo mkdir /cassandra_data
sudo mke2fs -F -F -O ^has_journal -t ext4 -b 4096 -E lazy_itable_init=0 /dev/sdb
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
